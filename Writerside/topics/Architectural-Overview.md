# Architectural Overview

We have designed our architecture based on the principles of Clean Architecture and Onion Architecture. The application
is divided into the following layers: Core, Use Case, Application, and Infrastructure/UI. Dependencies only flow inward
via dependency injection.

![architecture.jpg](architecture.jpg){ width="600" }

### Package structure

According to the defined architecture we have chosen the following package structure for the backend repository (public
transit service):

```
ch.naviqore/
- app/ (spring REST API)
- service/ (interfaces, service implementation and integration functionality)
    - PublicTransitService
         Stop
         Route
         Trip
         Connection
         Leg
         StopTime
    - implementation/ (of public transit service interface)
- core/
    - raptor/
        - RaptorAlgorithm (earliestArrical, rangeQuery, isoline, ...)
        - implementation/
            - plain-java/
            - native-jni/
    - gtfs/
        - GtfsRepository
        - static/
        - realtime/
    - utils/
- io/
    - gtfs/
```
