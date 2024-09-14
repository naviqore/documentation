# Sequence Diagram

The following sequence diagrams illustrate the key interactions and processes within the Naviqore system.

## Application Startup

This sequence diagram illustrates how the backend Spring application (REST API) initializes during the startup of the
Naviqore system. Upon startup, the **Public Transit Service** loads the **GTFS Static** schedule either from a file or a
URL. While running the service periodically updates the **GTFS Static** schedule from the given source.

```mermaid
sequenceDiagram
    participant Admin
    participant SpringApp as Spring Application (REST API)
    participant Service as Public Transit Service
    participant GTFS
    participant Schedule as GTFS Static

    Admin ->>+ SpringApp: Start
    SpringApp ->>+ Service: Initialize
    Service ->>+ GTFS: Load
    GTFS ->>+ Schedule: Fetch
    Schedule -->>- GTFS: Return data
    GTFS -->>- Service: Schedule in memory
    Service -->>- SpringApp: Ready

    loop Periodic GTFS Static Reload
        SpringApp ->>+ Service: Update GTFS Static
        Service ->>+ GTFS: Update
        GTFS ->>+ Schedule: Fetch new version
        Schedule -->>- GTFS: Return updated data
        GTFS -->>- Service: New schedule in memory
        Service -->>- SpringApp: Update complete
    end
   
     Admin ->> SpringApp: Stop
     SpringApp -->>- Admin: Shutdown complete

```

## Connection Request

This sequence diagram illustrates how the Naviqore system processes a connection request by a user. The system first
validates whether the requested stops are valid and retrieves parent or child stops if any. If the stops are valid,
the **Raptor** is used to query connections, and the connection results are enriched with information from the
**GTFS** before being returned to the user.

```mermaid
sequenceDiagram
    participant User
    participant UI as Web App UI
    participant API as REST API
    participant Service as Public Transit Service
    participant GTFS
    participant Raptor

    User ->>+ UI: Connection request
    UI ->>+ API: Forward request
    API ->>+ Service: Delegate request

    Service ->>+ GTFS: Validate stop ids
    GTFS -->>- Service: Stops

    alt Valid stops for connection query
        Service ->>+ Raptor: Query connections
        Raptor -->>- Service: Connection results
        
        Service ->>+ GTFS: Postprocess
        GTFS -->>- Service: Enriched connections
    end

    Service -->>- API: Return response
    API -->>- UI: Forward response
    UI -->>- User: Display results
```

