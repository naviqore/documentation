# Requirements

This page outlines the requirements for the Naviqore Public Transit Service and its User Interface (UI). The
requirements are categorized into *must-have*, *should-have*, and *nice-to-have* features. The *must-have* requirements
are essential and need to be met, while the *should-have* requirements are highly desirable and the *nice-to-have*
requirements are additional features that would enhance the service but are not critical.

Legend:

- UC: Use Case (Functional Requirement)
- NF: Non-function requirement

## Must-have

#### M: Service

- **UC-M1:** Efficiently (<250ms) find the nearest stops (beeline distance) with a limit (max 5km) with stop
  information (coordinates, name, routes).
- **UC-M2:** Find the next departures from a given stop with information (name, direction, if available headsign).
- **UC-M3:** Efficiently request (in mean <250ms) connections between two stops.
- **UC-M4:** The minimum transfer time can be set by the user in the connection routing request. Already provided
  transfer times from the public transit schedule should be preferred, but can optionally be overridden by the minimum
  transfer time set by the user.

- **NF-M1:** The complete service must be able to run on a normal machine (4 cores, 16GB).
- **NF-M2:** The prototype implementation of the service, router and gtfs reader is completely in Java.
- **NF-M3:** The communication with the service must be stateless (caching of results is still allowed).

#### M: Schedule

- **UC-M5:** Use the GTFS (General Transit Feed Specification) as input for the transit schedule.
- **UC-M6:** Read all required components from GTFS static schedule.
- **UC-M7:** Read optional transfers from GTFS and make them available to the router.

- **NF-M4:** The schedule is read into a memory-efficient structure, which takes less than 1.5GB (the size of the
  schedule file on disk) for all required fields of the GTFS Switzerland.

#### M: Routing

- **UC-9:** The routing algorithm RAPTOR (Round-Based Public Transit Routing) is used to find connections with the
  earliest arrival in the
  schedule, since its datastructures is optimized for cache locality.
- **UC-9:** The returned connection solutions have to be pareto-optimal (duration and number of transfers).
- **UC-14:** The integration in the performant programming language C++ with JNI is evaluated.

- **NF-5:** At least 5 manually chosen connections from the SBB app are used to validate the solutions from the
  algorithm.
- **NF-2:** Efficiency of random route requests is measured in relation to the complete transit schedule of Switzerland
  of 2024 in a benchmark test. The results are written to a file. The file must have a date-time stamp to be able to
  track the progress of the development.

#### M: Viewer

- **UC-5:** Simple frontend to display connections from origin to a destination stop for demo purposes.

## Should-have

#### S: Service

- **UC-11:** Update the static transit schedule at the defined interval (most often weekly) by the publisher (pull new
  GTFS static from URL and replace the current schedule in the service).

- **NF-12:** The public transit service should be able to process concurrent requests in parallel.
- **NF-3:** Containerized deployment ensures portability.
- **NF-3:** Open-Source release under a permissive or copy-left license.

#### S: Schedule

- **UC-13:** Apply the realtime GTFS updates on the static GTFS schedule at the defined interval (most often 2 minutes)
  by the publisher. Since the login procedure is different for every publisher, the focus is set on Switzerland.

#### S: Routing

- **UC-14:** Implement range queries (rRAPTOR) to find the connections with the earliest arrivals in a departure time
  window.
- **UC-14:** If the effort off the C++ implementation does not justify the performance gain, the JNI integration should
  be terminated based on this reasoning.
- **UC-14:** The routing should support isoline requests: How far can someone travel from an origin stop given a time
  budget.
- **UC-7:** A generic footpath routing interface is provided, which allows for extension of the router in the future.
- **UC-8:** Default implementation of footpath routing, which approximates the footpaths between stations with a
  sensible factor times the beeline distance.

#### S: Viewer

- **UC-15:** The connection routing results should be displaying on a map or line network graph.

## Nice-to-have

#### N: Service

- **UC-16:** Implement user accounts with login, which allows saving favorite connections in a database.
- **NF-16:** Horizontal scaling: Store the parsed static GTFS schedule and built Raptor data structures with a validity
  timestamp to a common storage (mounted volume or database), which is used by new instances of the service when
  started, instead of parsing the GTFS again.

- **NF-3:** The service should be horizontal scalable.
- **NF-10:** Deployment of public transit service in a cloud environment.

#### N: Schedule

- **UC-15:** Read the optional fares from the GTFS static schedule and make them availale to raptor.

#### N: Routing

- **UC-18:** Implementation of the footpath routing interface with a graph-based routing algorithm (e.g. A*Star or A*
  Landmark), that that uses a network read from OpenStreetMap data (e.g. from Geofabrik).
- **UC-17:** Supports efficient matrix route queries, and Raptor can potentially be optimized for this.
- **UC-14:** Implement multi-criteria queries (mcRAPTOR) to find the cheapest connections based on fares.

#### N: Viewer

- **UC-19:** A more sophisticated user interface, which is able to:
    - Explore and visualize the GTFS schedule.
    - Visualize the estimated vehicle positions from the GTFS realtime feed.
    - Display lines with departure times at selected stations.
    - Query connections using the Raptor-Router and display the results on a map.
    - Query reachability from a station within a given time budget.
    - Provide an option to visualize the functioning of the Raptor algorithm by visualizing the Raptor rounds until the
      target stop is reached.
