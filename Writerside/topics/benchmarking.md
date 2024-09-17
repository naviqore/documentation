# Benchmarking

## Extended Raptor for Production

According to **NF-RO-M2** the benchmarking of the extended Raptor algorithm (supporting multiday connections, querying
by departure or arrival times, and allowing for custom query criteria such as transport modes, number of transfers,
maximum walking distance, minimum transfer time, accessibility, or the possibility of carrying a bicycle) was conducted
using the current GTFS data for the whole of Switzerland and the results where continuously to versioned files, which
allowed to track the performance of our algorithm during development. The machine used for the benchmark meets the
requirements outlined in **NF-RO-M2**.

### Cache Locality

When iterating over the stop times in the route scanner of the Raptor algorithm, the router needs to access a large
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
was consumed by inserting new stops into the marked stops hashset in the main loop of the Raptor router. Since the set
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

TODO