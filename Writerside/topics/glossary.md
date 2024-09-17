# Glossary

In the context of this thesis, certain terms can have different meanings depending on whether they refer to public
transit in general, the RAPTOR algorithm, or GTFS. As a result, some terms are defined multiple times in the glossary to
reflect their specific usage in each area. While we aim for clarity in the text, some terms in the code may carry
different meanings depending on the layer or package they are associated with, even when the same term is used.

## Public Transit

| Term          | Description                                                                                                                        |
|---------------|------------------------------------------------------------------------------------------------------------------------------------|
| Agency        | An organization providing transit services.                                                                                        |
| Connection    | An option for travel that include details like fare and possible routes and transfers                                              |
| Leg           | A part of a connection in one mode of transportation or vehicle.                                                                   |
| Journey       | A connection is realized as a journey when the passenger selects it and begins traveling.                                          |
| Services      | Transit offerings by agencies, consisting of trips operating on specific routes.                                                   |
| Stop          | A location where passengers board or alight from transit vehicles.                                                                 |
| Schedule      | The planned timetable for transit services, detailing stops, routes, and times.                                                    |
| Transfer      | A switch between different routes or a footpath between two stops.                                                                 |
| Stop facility | Physical infrastructure where passengers wait and board transit vehicles.                                                          |
| Station       | A station is a large stop facility, typically serving rail. It can also consist multiple smaller stop facilities (e.g. platforms). |
| Platform      | A platform is a designated area within a station where passengers wait to board or alight from transit vehicles.                   |

## RAPTOR

| Term           | Description                                                                                                                                        |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Transfer       | *Same stop transfer*: Switching between routes at the same stop during a journey.                                                                  |
| Footpath       | *Between stop transfer*: A walking connection between two different stops that can be used during transfers.                                       |
| Round          | An iteration in the RAPTOR algorithm, evaluating routes and footpaths at each stop reached within the current number of allowed transfers.         |
| Route scanning | The process of evaluating possible transit routes that pass through marked stops to find optimal paths.                                            |
| Relaxing       | The process of applying footpaths to other stops connected to improved, marked stops in the current round.                                         |
| Marked stop    | A stop where the arrival time improved in the last round, requiring evaluation of routes or footpaths connected to this stop in the current round. |
| Pareto-optimal | A set of solutions where no journey is strictly worse in all criteria compared to any other journey.                                               |

## GTFS

The General Transit Feed Specification (GTFS), also known as GTFS static or static transit to differentiate it from the
GTFS realtime extension, defines a common format for public transportation schedules and associated geographic
information. GTFS "feeds" let public transit agencies publish their transit data and developers write applications that
consume that data in an interoperable way.

| Term                 | Description                                                                                                      | Assignment |
|----------------------|------------------------------------------------------------------------------------------------------------------|------------|
| Agency               | Transit agencies with service represented in this dataset.                                                       | GTFS       |
| Stops                | Stops where vehicles pick up or drop off riders. Also defines stations and station entrances.                    |            |
| Routes               | Transit routes. A route is a group of trips that are displayed to riders as a single service.                    |            |
| Trips                | Trips for each route. A trip is a sequence of two or more stops that occur during a specific time period.        |            |
| Stop times           | Times that a vehicle arrives at and departs from stops for each trip.                                            |            |
| Calendar             | Service dates specified using a weekly schedule with start and end dates.                                        |            |
| Calendar dates       | Exceptions for the services defined in the calendar.                                                             |            |
| Timeframes           | Date and time periods to use in fare rules for fares that depend on date and time factors.                       |            |
| Areas                | Area grouping of locations.                                                                                      |            |
| Stop areas           | Rules to assign stops to areas.                                                                                  |            |
| Networks             | Network grouping of routes.                                                                                      |            |
| Route networks       | Rules to assign routes to networks.                                                                              |            |
| Shapes               | Rules for mapping vehicle travel paths, sometimes referred to as route alignments.                               |            |
| Frequencies          | Headway (time between trips) for headway-based service or a compressed representation of fixed-schedule service. |            |
| Transfers            | Rules for making connections at transfer points between routes.                                                  |            |
| Pathways             | Pathways linking together locations within stations.                                                             |            |
| Levels               | Levels within stations.                                                                                          |            |
| Location groups      | A group of stops that together indicate locations where a rider may request pickup or drop off.                  |            |
| Location group stops | Rules to assign stops to location groups.                                                                        |            |
| Locations            | Zones for rider pickup or drop-off requests by on-demand services, represented as GeoJSON polygons.              |            |
| Booking rules        | Booking information for rider-requested services.                                                                |            |
| Translations         | Translations of customer-facing dataset values.                                                                  |            |
| Feed info            | Dataset metadata, including publisher, version, and expiration information.                                      |            |
| Leg                  | Travel in which a rider boards and alights between a pair of subsequent locations along a trip.                  |            |
| Journey              | Overall travel from origin to destination, including all legs and transfers in-between.                          |            |
| Sub-journey          | Two or more legs that comprise a subset of a journey.                                                            |            |
| Fare product         | Purchasable fare products that can be used to pay for or validate travel.                                        |            |
| Transit Route        | A group of trips, displayed to riders as a single service.                                                       |            |
