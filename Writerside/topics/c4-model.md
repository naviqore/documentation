# C4 Model

The C4 model is a simple, hierarchical way of visualizing software architecture. It consists of four layers:

- **System Context**: Shows how the system interacts with its environment.
- **Containers**: Defines high-level containers (applications, services, databases) that make up the system.
- **Components**: Focuses on the internal structure of each container, showing the components and how they communicate.
- **Code**: Zooms in on the details of individual components (often omitted in higher-level diagrams). In general, it is
  not recommended to create this layer, since it can be generated in modern IDEs.

## System Context

This diagram visualizes the Naviqore system and its main actors. These actors include the *User*, *Researcher*, and
*Public Transit Agency*, which interact with the system, and the GTFS schedule which is provided by the agency.

<!--
![structurizr-Context_Diagramm.png](structurizr-Context_Diagramm.png)
![structurizr-Context_Diagramm-key.png](structurizr-Context_Diagramm-key.png)
-->

```plantuml
@startuml
set separator none
title Naviqore System - System Context

left to right direction

skinparam {
  arrowFontSize 10
  defaultTextAlignment center
  wrapWidth 200
  maxMessageSize 100
}

hide stereotype

skinparam rectangle<<4>> {
  BackgroundColor #dddddd
  FontColor #000000
  BorderColor #9a9a9a
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem>> {
  BackgroundColor #1168bd
  FontColor #ffffff
  BorderColor #0b4884
  roundCorner 20
  shadowing false
}
skinparam person<<PublicTransitAgency>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}
skinparam person<<Researcher>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}
skinparam person<<User>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}

person "==User\n<size:10>[Person]</size>\n\nA simple every day user who wants to use public transit." <<User>> as User
person "==Researcher\n<size:10>[Person]</size>\n\nA professional who analyzes public transit and performs high volume routing requests." <<Researcher>> as Researcher
person "==Public Transit Agency\n<size:10>[Person]</size>\n\nA institution that offers public transit." <<PublicTransitAgency>> as PublicTransitAgency
rectangle "==GTFS Schedule\n\nA text file based representation of the operating schedule of one or more transit agencies." <<4>> as 4
rectangle "==Naviqore System\n<size:10>[Software System]</size>\n\nOur solution to statisfy all stakeholder needs" <<NaviqoreSystem>> as NaviqoreSystem

User .[#707070,thickness=2].> NaviqoreSystem : "<color:#707070>Requests connection"
User .[#707070,thickness=2].> NaviqoreSystem : "<color:#707070>Requests next departures from stop"
User .[#707070,thickness=2].> NaviqoreSystem : "<color:#707070>Requests closest stop"
Researcher .[#707070,thickness=2].> NaviqoreSystem : "<color:#707070>Requests isolines for stop"
NaviqoreSystem .[#707070,thickness=2].> 4 : "<color:#707070>Loads"
PublicTransitAgency .[#707070,thickness=2].> 4 : "<color:#707070>Provides"
@enduml
```

## Container

This diagram breaks down the Naviqore system into its primary containers. These include the *Web Application UI* and the
*Service*, which depend on the GTFS schedule to fulfill requests.

<!--
![structurizr-Diagram2.png](structurizr-Container_Diagram.png)
![structurizr-Diagram2-key.png](structurizr-Container_Diagram-key.png)
-->

```plantuml
@startuml
set separator none
title Naviqore System - Containers

left to right direction

skinparam {
  arrowFontSize 10
  defaultTextAlignment center
  wrapWidth 200
  maxMessageSize 100
}

hide stereotype

skinparam rectangle<<4>> {
  BackgroundColor #dddddd
  FontColor #000000
  BorderColor #9a9a9a
  roundCorner 20
  shadowing false
}
skinparam person<<Researcher>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.Service>> {
  BackgroundColor #438dd5
  FontColor #ffffff
  BorderColor #2e6295
  roundCorner 20
  shadowing false
}
skinparam person<<User>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.WebApplicationUI>> {
  BackgroundColor #438dd5
  FontColor #ffffff
  BorderColor #2e6295
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem>> {
  BorderColor #0b4884
  FontColor #0b4884
  shadowing false
}

person "==User\n<size:10>[Person]</size>\n\nA simple every day user who wants to use public transit." <<User>> as User
person "==Researcher\n<size:10>[Person]</size>\n\nA professional who analyzes public transit and performs high volume routing requests." <<Researcher>> as Researcher
rectangle "==GTFS Schedule\n\nA text file based representation of the operating schedule of one or more transit agencies." <<4>> as 4

rectangle "Naviqore System\n<size:10>[Software System]</size>" <<NaviqoreSystem>> {
  rectangle "==Web Application UI\n<size:10>[Container: Python / Streamlit]</size>\n\nEasy to use website with forms to request and view connections." <<NaviqoreSystem.WebApplicationUI>> as NaviqoreSystem.WebApplicationUI
  rectangle "==Service\n<size:10>[Container: Spring]</size>\n\nService that contains all the required data and algorithms to respond to incoming requests." <<NaviqoreSystem.Service>> as NaviqoreSystem.Service
}

User .[#707070,thickness=2].> NaviqoreSystem.WebApplicationUI : "<color:#707070>Requests information"
Researcher .[#707070,thickness=2].> NaviqoreSystem.Service : "<color:#707070>Sends requests"
NaviqoreSystem.WebApplicationUI .[#707070,thickness=2].> NaviqoreSystem.Service : "<color:#707070>Sends requests"
NaviqoreSystem.Service .[#707070,thickness=2].> 4 : "<color:#707070>Loads"
@enduml
```

## Component

This diagram drills into the Service container, showing its key internal components such as the *Raptor*, *GTFS*, *REST
API*, and *Public Transit Service*.

<!--
![structurizr-Service_Components.png](structurizr-Service_Components.png)
![structurizr-Service_Components-key.png](structurizr-Service_Components-key.png)
--> 

```plantuml
@startuml
set separator none
title Naviqore System - Service - Components

left to right direction

skinparam {
  arrowFontSize 10
  defaultTextAlignment center
  wrapWidth 200
  maxMessageSize 100
}

hide stereotype

skinparam rectangle<<NaviqoreSystem.Service.GTFS>> {
  BackgroundColor #85bbf0
  FontColor #000000
  BorderColor #5d82a8
  roundCorner 20
  shadowing false
}
skinparam rectangle<<4>> {
  BackgroundColor #dddddd
  FontColor #000000
  BorderColor #9a9a9a
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.Service.PublicTransitService>> {
  BackgroundColor #85bbf0
  FontColor #000000
  BorderColor #5d82a8
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.Service.RESTAPI>> {
  BackgroundColor #85bbf0
  FontColor #000000
  BorderColor #5d82a8
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.Service.Raptor>> {
  BackgroundColor #85bbf0
  FontColor #000000
  BorderColor #5d82a8
  roundCorner 20
  shadowing false
}
skinparam person<<Researcher>> {
  BackgroundColor #08427b
  FontColor #ffffff
  BorderColor #052e56
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.WebApplicationUI>> {
  BackgroundColor #438dd5
  FontColor #ffffff
  BorderColor #2e6295
  roundCorner 20
  shadowing false
}
skinparam rectangle<<NaviqoreSystem.Service>> {
  BorderColor #2e6295
  FontColor #2e6295
  shadowing false
}

person "==Researcher\n<size:10>[Person]</size>\n\nA professional who analyzes public transit and performs high volume routing requests." <<Researcher>> as Researcher
rectangle "==GTFS Schedule\n\nA text file based representation of the operating schedule of one or more transit agencies." <<4>> as 4
rectangle "==Web Application UI\n<size:10>[Container: Python / Streamlit]</size>\n\nEasy to use website with forms to request and view connections." <<NaviqoreSystem.WebApplicationUI>> as NaviqoreSystem.WebApplicationUI

rectangle "Service\n<size:10>[Container: Spring]</size>" <<NaviqoreSystem.Service>> {
  rectangle "==Raptor\n<size:10>[Component: Java]</size>\n\nHolds a reduced compact performant copy of the schedule in memory and calulates routes efficiently using the raptor algorithm." <<NaviqoreSystem.Service.Raptor>> as NaviqoreSystem.Service.Raptor
  rectangle "==GTFS\n<size:10>[Component: Java]</size>\n\nHolds the entire GTFS schedule in memory." <<NaviqoreSystem.Service.GTFS>> as NaviqoreSystem.Service.GTFS
  rectangle "==REST API\n<size:10>[Component: Spring]</size>\n\nOutwards facing interface of the service" <<NaviqoreSystem.Service.RESTAPI>> as NaviqoreSystem.Service.RESTAPI
  rectangle "==Public Transit Service\n<size:10>[Component: Java]</size>\n\nOrchestrates the service, pulls external data, creates and caches instances of router and schedule and pre-/post-processes requests." <<NaviqoreSystem.Service.PublicTransitService>> as NaviqoreSystem.Service.PublicTransitService
}

NaviqoreSystem.WebApplicationUI .[#707070,thickness=2].> NaviqoreSystem.Service.RESTAPI : "<color:#707070>Sends requests"
Researcher .[#707070,thickness=2].> NaviqoreSystem.Service.RESTAPI : "<color:#707070>Sends requests"
NaviqoreSystem.Service.RESTAPI .[#707070,thickness=2].> NaviqoreSystem.Service.PublicTransitService : "<color:#707070>Delegates requests"
NaviqoreSystem.Service.PublicTransitService .[#707070,thickness=2].> NaviqoreSystem.Service.Raptor : "<color:#707070>Has"
NaviqoreSystem.Service.PublicTransitService .[#707070,thickness=2].> NaviqoreSystem.Service.GTFS : "<color:#707070>Has"
NaviqoreSystem.Service.PublicTransitService .[#707070,thickness=2].> 4 : "<color:#707070>Uses to create GTFS instance"
@enduml
```

<!--
// https://structurizr.com/dsl

workspace {

    model {
        user = person "User" {
            description "A simple every day user who wants to use public transit."
        }
        researcher = person "Researcher" {
            description "A professional who analyzes public transit and performs high volume routing requests."
        }
        agency = person "Public Transit Agency" {
            description "A institution that offers public transit."
        }
        gtfsSchedule = element "GTFS Schedule" {
            description "A text file based representation of the operating schedule of one or more transit agencies."
        }
        
        
        softwareSystem = softwareSystem "Naviqore System" {
            description "Our solution to statisfy all stakeholder needs"
            wa = container "Web Application UI" "Streamlit User Interface" {
                technology "Python / Streamlit"
                description "Easy to use website with forms to request and view connections."
            }
            service = container "Service" "Spring Service with REST API Endpoints" {
                technology "Spring"
                description "Service that contains all the required data and algorithms to respond to incoming requests."
                springApp = component "REST API" {
                    technology "Spring"
                    description "Outwards facing interface of the service"
                }
                publicTransitService = component "Public Transit Service" {
                    technology "Java"
                    description "Orchestrates the service, pulls external data, creates and caches instances of router and schedule and pre-/post-processes requests."
                }
                raptor = component "Raptor" {
                    technology "Java"
                    description "Holds a reduced compact performant copy of the schedule in memory and calulates routes efficiently using the raptor algorithm."
                }
                gtfs = component "GTFS" {
                    technology "Java"
                    description "Holds the entire GTFS schedule in memory."
                }
            }
        }
        


        // context diagram
        user -> softwareSystem "Requests connection"
        user -> softwareSystem "Requests next departures from stop"
        user -> softwareSystem "Requests closest stop"
        researcher -> softwareSystem "Requests isolines for stop"
        softwareSystem -> gtfsSchedule "Loads"
        agency -> gtfsSchedule "Provides"
        
        // container diagramm
        user -> wa "Requests information"
        researcher -> service "Sends requests"
        wa -> service "Sends requests"
        service -> gtfsSchedule "Loads"
        
        // service components diagramm
        wa -> springApp "Sends requests"
        researcher -> springApp "Sends requests"
        springApp -> publicTransitService "Delegates requests"
        publicTransitService -> raptor "Has"
        publicTransitService -> gtfs "Has"
        publicTransitService -> gtfsSchedule "Uses to create GTFS instance"
    }

    views {
        systemContext softwareSystem "Context_Diagramm" {
            include * agency
            autolayout lr
        }

        container softwareSystem "Diagram2" {
            include *
            autolayout lr
        }
        
        component service "Service_Components" {
            include *
            autolayout lr
        }
        
        theme default
    }

}
-->