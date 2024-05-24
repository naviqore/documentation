# Use Case

## User Perspective

```plantuml

@startuml
left to right direction
actor User

User --> (View Schedule)
User --> (Set Preferences)
User --> (View Transit Information)
User --> (Plan Transit Journey)
@enduml

```

## Agency Perspective

```plantuml
@startuml
left to right direction
actor TransitAgency
actor GTFSValidator

TransitAgency --> (Publish Transit Data)
TransitAgency --> (Update Transit Data)
GTFSValidator --> (Validate GTFS Data)
TransitAgency --> GTFSValidator : provides GTFS data
@enduml
```
