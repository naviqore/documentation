# Benchmarking

## Extended Raptor for Production

According to **NF-RO-M2** the benchmarking of the extended Raptor algorithm (supporting multiday connections, querying
by departure or arrival times, and allowing for custom query criteria such as transport modes, number of transfers,
maximum walking distance, minimum transfer time, accessibility, or the possibility of carrying a bicycle) was conducted
using the current GTFS data for the whole of Switzerland and the results where continuously to versioned files, which
allowed to track the performance of our algorithm during development. The machine used for the benchmark meets the
requirements outlined in **NF-RO-M2**.

### Cache locality

TODO: Add performance increase description due to cache locality in the stop time array.

### v1.0.0

The benchmark results are visualized in nine plots. Processing time is shown to increase with both the number of
transfers and the number of connection results, with median times remaining under 150 ms for most cases. The histogram
of processing times reveals a mean of 98.16 ms and a median of 99.00 ms per request, confirming efficient connection
query handling. Scatter plots show a weak positive correlation between processing time and both beeline distance and
connection duration. Most queries involve 1–2 transfers (80%), and departure time accuracy is high, with minimal
deviation between requested and actual times.

![v1.0.0 - Benchmark Results](2024_09_10_benchmark_lenovo.png)

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