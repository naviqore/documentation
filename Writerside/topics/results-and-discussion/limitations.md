# Limitations

While this thesis demonstrates the potential and applicability of RAPTOR for public transit routing using GTFS data,
there are several limitations to the approach and implementation that need to be acknowledged.

One significant limitation is the absence of useful optional components in the GTFS publications by various national
transit agencies. While the mandatory fields are generally present, many agencies do not provide certain optional fields
that could enhance the service's capabilities. For example, the Swiss GTFS data lacks some footpaths between stops, even
though these transfers are possible. Additionally, there is no information regarding accessibility features
or bike transportation, which limits the service's adaptability for users with specific needs.

International routing presents another significant challenge, as it requires working with multiple GTFS feeds. Merging
datasets from regions within the same timezone is technically feasible but introduces its own complexity, such as
resolving duplicate routes and stops that may have different identifiers. When dealing with multiple timezones,
all stop times and calendar dates must be converted to UTC before merging schedules.

The trade-off between memory usage and performance is another limitation of the system. Our RAPTOR router requires a
significant amount of memory, particularly for building and caching various stop time arrays, as a new array is
generated for each combination of service days, transport modes, accessibility options, and bike transport settings.
However, as the size of the GTFS dataset increases, so does the cache, potentially leading to memory exhaustion. In
resource-constrained environments, the cache size must be reduced, negatively impacting performance, especially when
users request a wide range of query combinations.

Additionally, the implementation of RAPTOR++ in C++ brought several technical obstacles. The complexity of working with
the Foreign Function and Memory (FFM) API, multi-operating system builds, and dependency management through CMake and
vcpkg presented significant hurdles. Moreover, setting up a logging framework without introducing dependencies
throughout the project required extensive effort, with the bridge pattern ultimately being adopted to isolate logging
logic.

Lastly, the initial goal of using the FFM API to pass routing requests from the benchmarking setup to the C++ RAPTOR was
abandoned. The need to reduce the complex RAPTOR data structures in Java to primitive types for the API, and then
rebuild them on the C++ side, would have significantly impacted performance. Consequently, the C++ benchmarking was
conducted independently of the Java implementation.
