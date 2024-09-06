# Architectural Overview

We have designed our architecture based on the principles of Clean Architecture and Onion Architecture. The application
is divided into the following layers: Core, Use Case, Application, and Infrastructure/UI. Dependencies only flow inward
via dependency injection.

![architecture.jpg](architecture.jpg){ width="600" }

## Package structure

According to the defined architecture we have chosen the following package structure for the backend repository (public
transit service):

```
.
└── ch.naviqore
    ├── app (spring REST API)
    │         ├── infrastructure (implementations of the service schedule repository)
    │         └── ...
    ├── service (interfaces)
    │         ├── gtfs
    │         │         └── raptor (service implementation and integration functionality)
    │         ├── repo (interface to access schedules)
    │         └── ...
    ├── gtfs
    │         └── schedule
    ├── raptor (algorithm interfaces)
    │         ├── router (implementation fo the raptor algorithm)
    │         └── ... (further raptor versions for benchmarking, via Foreign Function and Memory API)
    └── utils (spatial data types and indices, search trie, networking, ...)
```
