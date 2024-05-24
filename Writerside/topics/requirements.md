# Requirements

This page outlines the requirements for the Naviqore Public Transit Service and its User Interface (UI). The
requirements are categorized into *must-have*, *should-have*, and *nice-to-have* features. The *must-have* requirements
are essential and need to be met, while the *should-have* requirements are highly desirable and the *nice-to-have*
requirements are additional features that would enhance the service but are not critical.

Type:

- `UC`: Use case
- `NF`: Non-function requirement

Component:

- `SE`: Service
- `SC`: Schedule
- `RO`: Routing
- `VW`: Viewer

Priority:0

- `M`: Must-have
- `S`: Should-have
- `N`: Nice-to-have

Requirement ID = `{TYPE}-{COMPONENT}-{PRIORITY}{NUMBER}`

## Must-have

| ID           | Description                                                                                                                                                                                                                                                           |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UC-SE-M1** | Efficiently (<250ms) find the nearest stops (beeline distance) with a limit (max 5km) with stop information (coordinates, name, routes).                                                                                                                              |
| **UC-SE-M2** | Find the next departures from a given stop with information (name, direction, if available head-sign).                                                                                                                                                                |
| **UC-SE-M3** | Efficiently request (in mean <250ms) connections between two stops.                                                                                                                                                                                                   |
| **UC-SE-M4** | The minimum transfer time can be set by the user in the connection routing request. Already provided transfer times from the public transit schedule should be preferred, but can optionally be overridden by the minimum transfer time set by the user.              |
| **NF-SE-M1** | The complete service must be able to run on a normal machine (8 cores, 16GB).                                                                                                                                                                                         |
| **NF-SE-M2** | The prototype implementation of the service, router, and GTFS reader is completely in Java.                                                                                                                                                                           |
| **NF-SE-M3** | The communication with the service must be stateless (caching of results is still allowed).                                                                                                                                                                           |
| **UC-SC-M1** | Use the GTFS (General Transit Feed Specification) as input for the transit schedule.                                                                                                                                                                                  |
| **UC-SC-M2** | Read all required components from GTFS static schedule.                                                                                                                                                                                                               |
| **UC-SC-M3** | Read optional transfers from GTFS and make them available to the router.                                                                                                                                                                                              |
| **NF-SC-M1** | The schedule is read into a memory-efficient structure, which takes less than 1.5GB (the size of the schedule file on disk) for all required fields of the GTFS Switzerland.                                                                                          |
| **UC-RO-M1** | The routing algorithm RAPTOR (Round-Based Public Transit Routing) is used to find connections with the earliest arrival in the schedule, as its data structures are optimized for cache locality.                                                                     |
| **UC-RO-M2** | The returned connection solutions have to be pareto-optimal (duration and number of transfers).                                                                                                                                                                       |
| **UC-RO-M3** | The integration in the performant programming language C++ with JNI is evaluated.                                                                                                                                                                                     |
| **NF-RO-M1** | At least 5 manually chosen connections from the SBB app are used to validate the solutions from the algorithm.                                                                                                                                                        |
| **NF-RO-M2** | Efficiency of random route requests is measured in relation to the complete transit schedule of Switzerland of 2024 in a benchmark test. The results are written to a file. The file must have a date-time stamp to be able to track the progress of the development. |
| **UC-VW-M1** | Simple frontend to display connections from origin to a destination stop for demo purposes.                                                                                                                                                                           |

## Should-have

| ID           | Description                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UC-SE-S1** | Update the static transit schedule at the defined interval (most often weekly) by the publisher (pull new GTFS static from URL and replace the current schedule in the service).                                          |
| **NF-SE-S1** | The public transit service should be able to process concurrent requests in parallel.                                                                                                                                     |
| **NF-SE-S2** | Containerized deployment ensures portability.                                                                                                                                                                             |
| **NF-SE-S3** | Open-Source release under a permissive or copy-left license.                                                                                                                                                              |
| **UC-SC-S1** | Apply the realtime GTFS updates on the static GTFS schedule at the defined interval (most often 2 minutes) by the publisher. Since the login procedure is different for every publisher, the focus is set on Switzerland. |
| **UC-RO-S1** | Implement range queries (rRAPTOR) to find the connections with the earliest arrivals in a departure time window.                                                                                                          |
| **UC-RO-S2** | If the effort of the C++ implementation does not justify the performance gain, the JNI integration should be terminated based on this reasoning.                                                                          |
| **UC-RO-S3** | The routing should support isoline requests: How far can someone travel from an origin stop given a time budget.                                                                                                          |
| **UC-RO-S4** | A generic footpath routing interface is provided, which allows for extension of the router in the future.                                                                                                                 |
| **UC-RO-S5** | Default implementation of footpath routing, which approximates the footpaths between stations with a sensible factor times the beeline distance.                                                                          |
| **UC-VW-S1** | The connection routing results should be displayed on a map or line network graph.                                                                                                                                        |

## Nice-to-have

| ID             | Description                                                                                                                                                                                                                                                           |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UC-SE-N1**   | Implement user accounts with login, which allows saving favorite connections in a database.                                                                                                                                                                           |
| **NF-SE-N1**   | Horizontal scaling: Store the parsed static GTFS schedule and built Raptor data structures with a validity timestamp to a common storage (mounted volume or database), which is used by new instances of the service when started, instead of parsing the GTFS again. |
| **NF-SE-N2**   | The service should be horizontally scalable.                                                                                                                                                                                                                          |
| **NF-SE-N3**   | Deployment of public transit service in a cloud environment.                                                                                                                                                                                                          |
| **UC-SC-N1**   | Read the optional fares from the GTFS static schedule and make them available to Raptor.                                                                                                                                                                              |
| **UC-RO-N1**   | Implementation of the footpath routing interface with a graph-based routing algorithm (e.g. A*Star or A* Landmark), that uses a network read from OpenStreetMap data (e.g. from Geofabrik).                                                                           |
| **UC-RO-N2**   | Supports efficient matrix route queries, and Raptor can potentially be optimized for this.                                                                                                                                                                            |
| **UC-RO-N3**   | Implement multi-criteria queries (mcRAPTOR) to find the cheapest connections based on fares.                                                                                                                                                                          |
| **UC-VW-N1**   | A more sophisticated user interface.                                                                                                                                                                                                                                  |
| **UC-VW-N1.1** | Explore and visualize the GTFS schedule.                                                                                                                                                                                                                              |
| **UC-VW-N1.2** | Visualize the estimated vehicle positions from the GTFS realtime feed.                                                                                                                                                                                                |
| **UC-VW-N1.3** | Display lines with departure times at selected stations.                                                                                                                                                                                                              |
| **UC-VW-N1.4** | Query connections using the Raptor-Router and display the results on a map.                                                                                                                                                                                           |
| **UC-VW-N1.5** | Query reachability from a station within a given time budget.                                                                                                                                                                                                         |
| **UC-VW-N1.6** | Provide an option to visualize the functioning of the Raptor algorithm by visualizing the Raptor rounds until the target stop is reached.                                                                                                                             |
