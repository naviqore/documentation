# Benchmarking

## Extended RAPTOR for Production

According to **NF-RO-M2** the benchmarking of the extended RAPTOR algorithm (supporting multi-day connections, querying
by departure or arrival times, and allowing for custom query criteria such as transport modes, number of transfers,
maximum walking distance, minimum transfer time, accessibility, or the possibility of carrying a bicycle) was conducted
using the current GTFS data for the whole of Switzerland and the results where continuously to versioned files, which
allowed to track the performance of our algorithm during development. The machine used for the benchmark meets the
requirements outlined in **NF-RO-M2**.

### Cache Locality

When iterating over the stop times in the route scanner of the RAPTOR algorithm, the router needs to access a large
number of integer values sequentially to determine whether a transfer to another trip from the currently active trip is
possible. Initially, we followed the structure described in the original paper and created an array of `StopTime`
objects, where each stop time consisted of both an arrival and departure time encapsulated in a record class.

However, in Java, this approach meant iterating over an array of references to `StopTime` objects stored on the heap.
While the CPU cache would prefetch multiple adjacent memory addresses when reading from the array of references,
accessing the actual `StopTime` objects still required fetching data from scattered memory locations on the heap, which
is relatively costly in terms of memory access latency.

To optimize this, we refactored the data structure by replacing the array of `StopTime` objects with a single integer
array containing the raw arrival and departure times for all trips. In Java, arrays of primitive types, such as
integers, are stored sequentially in memory. This change significantly improved cache locality, as iterating over the
array of integers allowed the CPU to efficiently utilize its cache. As a result, we observed a considerable performance
gain. However, this optimization came at the cost of some readability and maintainability, as accessing the arrival and
departure times now requires knowledge of the array structure to compute the correct indices.

TODO: Add performance increase numbers.

### Hashset vs. Boolean Mask Array

During profiling of connection requests, it was discovered that approximately 25% of the CPU time per routing request
was consumed by inserting new stops into the marked stops hashset in the main loop of the RAPTOR router. Since the set
of marked stops is relatively small, we hypothesized that frequent collisions might occur in the hash function, leading
to inefficiencies. However, attempts to optimize the hash function did not result in significant performance gains.

To address this, we replaced the hashset with a boolean array, where each index corresponds to a stop, and stops to be
scanned in the next round are flagged as true. This improved performance considerably, reducing the time per request
from 76ms to 48ms, a 37% performance improvement, on the GTFS dataset for Switzerland.

### v1.0.0

The benchmark results are visualized in nine plots. Processing time is shown to increase with both the number of
transfers and the number of connection results, with median times remaining under 100 ms for most cases. The histogram
of processing times reveals a mean of 48 ms and a median of 50 ms per request, confirming efficient connection
query handling. Scatter plots show a positive correlation between processing time and both beeline distance and
connection duration. Most queries involve 1–2 transfers (80%), and departure time accuracy is high, with minimal
deviation between requested and actual times.

![v1.0.0 - Benchmark Results](2024_09_17_benchmark_lenovo.png)

In regular use, on a large public transit schedule dataset on an average machine, the router performs efficiently and
fully satisfies the requirements **UC-SE-M3** (*Efficiently request connections between two stops,in mean <250ms.*)
and **NF-SE-M1** (*The complete service for Switzerland must be able to run on a standard machine with 8 cores and 16GB
of RAM.*)

As specified in **NF-RO-M1**, more than five connections were manually validated using the SBB app as a reference. There
were generally no discrepancies, and when differences did occur, they were attributable to service configuration
settings, such as minimum transfer times or maximum walking distances. Requirement **UC-RO-M2** is also fulfilled, as
all compared connection results are Pareto-optimal.

## Raptor Versions for Comparison

After adding multiple configurations for the RAPTOR algorithm, it was interesting to compare the performance of
different configurations. All of the compared configurations were benchmarked with 1000 identical routing requests.

### Tested RAPTOR implementations

The RAPTOR implementations compared are as follows:

#### Simple RAPTOR

A minimal implementation of the algorithm, without support for multi-service days (no `TripMaskProvider`) and only
supporting earliest arrival queries. Since it only includes routes and trips operating on the selected service day (
i.e., service day-specific RAPTOR data), the number of routes and stop times is reduced. This results in fewer checks
and lookups, making this version expected to be the fastest.

#### Regular Extended RAPTOR

This version operates on the same core code as the following implementations but is configured in the most basic way. It
does not support departure ranges (i.e., no Range RAPTOR) and does not use multi-day masks (only loading the service day
mask for the active day). This should be the fastest of the "extended" implementations.

#### Multi-Day RAPTORs

For these tests, the range was set to 0, and different numbers of days were scanned. Here, "1 day" refers to scanning
only the active service day, "2 days" means scanning the active and previous day, and everything greater than "3 days",
means scanning the previous, the current and n-2 days in the future. Since the 1 day RAPTOR would be equal to the "
regular" RAPTOR implementation, only 3 and 5 day RAPTORS were added.

#### Range RAPTORs

Basic Range RAPTORs were run with different range values but without multi-day masks. The following ranges were tested:

- `range_1800`: Range set to 30 minutes (1800 seconds)
- `range_3600`: Range set to 1 hour (3600 seconds)
- `range_7200`: Range set to 2 hours (7200 seconds)
- `range_14400`: Range set to 4 hours (14400 seconds)

#### Multi-Day Range RAPTORs

To assess the impact of combining multi-day scans and range RAPTORs, the same range values used in the Range RAPTOR
tests were tested again, but with the scan set to 3 days.

### Results and Discussions

As expected, the Simple RAPTOR implementation was the fastest, with an average runtime of 32 ms (± 21 ms), since it
required the fewest comparisons and lookups. The additional overhead of loading the full stop times array and masking
non-active trips with Integer.MIN_VALUE added around 7 ms, resulting in an average of 39 ms (± 25 ms).

The performance comparison between Range RAPTOR and Multi-Day RAPTOR was more intriguing. Adding small ranges to the
RAPTOR configuration did not significantly increase computational time (+7% for a 30-minute range, +42% for a 1-hour
range). This can be attributed to the benchmarking process, which sampled stops randomly across Switzerland. Small stops
with limited service were overrepresented, leading to fewer departures within the specified range, and often resulting
in scanning only one set of departures. However, for larger ranges, the cost became more pronounced (+112% for a 2-hour
range, +287% for a 4-hour range).

Similarly, increasing the number of days to scan had a noticeable but less dramatic impact. Scanning across 3 days (the
previous, current, and next day) increased the runtime by +48%, while scanning across 5 days resulted in a 100% increase
in runtime.

When combining both range and multi-day scans in one RAPTOR implementation, the performance costs were cumulative, as
both factors added their respective overheads.

![Router Comparison](boxplot_processing_time.png)

| router_id         | count | mean (ms) | std (ms) | median (ms) | max (ms) |
|:------------------|------:|----------:|---------:|------------:|---------:|
| simple            |  1000 |        32 |       21 |          34 |      135 |
| regular           |  1000 |        39 |       25 |          42 |      123 |
| 3_day             |  1000 |        58 |       28 |          62 |      144 |
| 5_day             |  1000 |        78 |       36 |          80 |      218 |
| range_1800        |  1000 |        42 |       29 |          43 |      163 |
| range_3600        |  1000 |        55 |       44 |          48 |      282 |
| range_7200        |  1000 |        83 |       76 |          59 |      525 |
| range_14400       |  1000 |       151 |      152 |          98 |      828 |
| 3_day_range_1800  |  1000 |        59 |       31 |          60 |      175 |
| 3_day_range_3600  |  1000 |        74 |       47 |          67 |      296 |
| 3_day_range_7200  |  1000 |       113 |       86 |          90 |      562 |
| 3_day_range_14400 |  1000 |       198 |      170 |         149 |      930 |

Of course, adding more features to the RAPTOR algorithm not only increased computational costs but also provided better
results and enhanced flexibility for more specific queries (e.g., travel modes, wheelchair accessibility, etc.). Most
notably, the **Range RAPTOR** enabled finding more time-efficient connections by allowing later departures while still
achieving the same earliest arrival. Meanwhile, the **Multi-Day RAPTOR** made it possible to find earlier arrivals, as
trips from the previous service day could be utilized. It also increased the success rate for connections with limited
service, where trips from the following days were necessary.

The table and figure below illustrate these results:

- **Success rate**: the percentage of requests that successfully found a connection between the departure and arrival
  stops.
- **Earliest arrival rate**: the proportion of requests that resulted in the earliest possible arrival.
- **Shortest duration rate**: the percentage of requests that returned the latest possible departure with the shortest
  overall travel time.

![Router Success Rates](success_rates.png)

| raptor_id         | Successful | Shortest Duration | Earliest Arrival |
|:------------------|-----------:|------------------:|-----------------:|
| simple            |        69% |               44% |              69% |
| regular           |        69% |               44% |              69% |
| 3_day             |        89% |               55% |              89% |
| 5_day             |        97% |               63% |              97% |
| range_1800        |        69% |               48% |              69% |
| range_3600        |        69% |               55% |              69% |
| range_7200        |        69% |               61% |              69% |
| range_14400       |        69% |               69% |              69% |
| 3_day_range_1800  |        89% |               58% |              89% |
| 3_day_range_3600  |        89% |               66% |              89% |
| 3_day_range_7200  |        89% |               74% |              89% |
| 3_day_range_14400 |        89% |               88% |              89% |

In summary, adding a greater range and more days to scan significantly improves the routing responses. However, this
effect is somewhat biased due to the dataset used, which includes many small stops with only a few departures per week.
This makes the impact of adding larger ranges and more days appear more extreme. In contrast, the differences would be
less pronounced in an urban network with high-frequency service.

Therefore, when configuring the RAPTOR algorithm, it's important to select parameters based on the characteristics of
the typical user and the specific transit network being routed, to ensure optimal performance.

## C++ Benchmarking

TODO: Comparison with Java Simple Raptor