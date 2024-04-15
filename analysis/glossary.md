# Glossary

## Public transit

## RAPTOR

## GTFS

The General Transit Feed Specification (GTFS), also known as GTFS static or static transit to differentiate it from the
GTFS realtime extension, defines a common format for public transportation schedules and associated geographic
information. GTFS "feeds" let public transit agencies publish their transit data and developers write applications that
consume that data in an interoperable way.

| Term                 | Description                                                                                                      |
|----------------------|------------------------------------------------------------------------------------------------------------------|
| Agency               | Transit agencies with service represented in this dataset.                                                       |
| Stops                | Stops where vehicles pick up or drop off riders. Also defines stations and station entrances.                    |
| Routes               | Transit routes. A route is a group of trips that are displayed to riders as a single service.                    |
| Trips                | Trips for each route. A trip is a sequence of two or more stops that occur during a specific time period.        |
| Stop times           | Times that a vehicle arrives at and departs from stops for each trip.                                            |
| Calendar             | Service dates specified using a weekly schedule with start and end dates.                                        |
| Calendar dates       | Exceptions for the services defined in the calendar.                                                             |
| Timeframes           | Date and time periods to use in fare rules for fares that depend on date and time factors.                       |
| Areas                | Area grouping of locations.                                                                                      |
| Stop areas           | Rules to assign stops to areas.                                                                                  |
| Networks             | Network grouping of routes.                                                                                      |
| Route networks       | Rules to assign routes to networks.                                                                              |
| Shapes               | Rules for mapping vehicle travel paths, sometimes referred to as route alignments.                               |
| Frequencies          | Headway (time between trips) for headway-based service or a compressed representation of fixed-schedule service. |
| Transfers            | Rules for making connections at transfer points between routes.                                                  |
| Pathways             | Pathways linking together locations within stations.                                                             |
| Levels               | Levels within stations.                                                                                          |
| Location groups      | A group of stops that together indicate locations where a rider may request pickup or drop off.                  |
| Location group stops | Rules to assign stops to location groups.                                                                        |
| Locations            | Zones for rider pickup or drop-off requests by on-demand services, represented as GeoJSON polygons.              |
| Booking rules        | Booking information for rider-requested services.                                                                |
| Translations         | Translations of customer-facing dataset values.                                                                  |
| Feed info            | Dataset metadata, including publisher, version, and expiration information.                                      |
| Leg                  | Travel in which a rider boards and alights between a pair of subsequent locations along a trip.                  |
| Journey              | Overall travel from origin to destination, including all legs and transfers in-between.                          |
| Sub-journey          | Two or more legs that comprise a subset of a journey.                                                            |
| Fare product         | Purchassable fare products that can be used to pay for or validate travel.                                       |
| Transit Route        | A group of trips, displayed to riders as a single service.                                                       |

### Schedule

### Realtime

