# Architectural Overview

We have designed our architecture based on the principles of Clean Architecture and Onion Architecture. The application
is divided into the following layers: Core, Use Case, Application, and Infrastructure/UI. Dependencies only flow inward
via dependency injection.

![architecture.jpg](architecture.jpg){ width="600" }

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

Since we have adopted an onion architecture, all dependencies point inward. The outer layers interact with abstractions
defined in the inner layers or implement interfaces provided by the inner layers. Each layer exposes a set of public
interfaces, serving as its outward-facing API. This architecture promotes loose coupling because the implementation of
any layer can be changed without requiring modifications to the outer layers.

For example, the service layer provides the `PublicTransitService` interface along with relevant parameter and return
types, such as `ConnectionQueryConfig` and `Connection`. The actual implementation of this
service, `GtfsRaptorService`, is abstracted away from the application layer, making it easily replaceable. In the
application layer, `PublicTransitSpringService` also implements the `PublicTransitService` interface and uses the
delegate pattern to forward requests from the REST controllers to the service. This encapsulates all the Spring
components, configurations, and dependencies within the outermost app layer, keeping them isolated from the service and
core logic.

Similarly, the `GtfsScheduleRepository` interface in the service layer is implemented in the application layer by
classes such as `GtfsScheduleFile` and `GtfsScheduleUrl`. For the service itself, it is not relevant how the GTFS
schedule is provided, as it only expects a concrete implementation of the repository interface from the instantiator,
which is responsible for providing the GTFS schedule.

This concept is applied consistently across the project, with a few deliberate exceptions. One notable drawback of this
architecture is that each layer defines its own representation of the same real-world entities, leading to frequent type
mapping as requests and responses traverse the layers. A good example is the entity of a transit stop, which is
abstracted differently in various layers. In the core layer, we maintain two distinct abstractions: one for GTFS stops
and another for stops used by the Raptor algorithm. This separation exists because the concept of a transit stop differs
based on the context of the layer. For instance, in the GTFS layer, technical details such as possible transfers are
prioritized, while in the service layer, information from the passenger’s perspective, such as the stop’s full name and
available routes, takes precedence. In these cases, maintaining separate abstractions for transit stops is justified due
to the distinct roles they play across layers.

However, for more stable concepts like locations and coordinates, a unified representation suffices across all layers.
Instead of duplicating these entities within each layer, we extracted them into a cross-cutting `utils.spatial` module.
These data types are shared across layers without any need for mapping, improving both performance and maintainability.