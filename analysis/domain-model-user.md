# Domain model

```mermaid
classDiagram
    class User {

    }
    class Journey {

    }
    class Leg {

    }
    class Transfer {

    }

    User "1" --> "0..*" Journey: requests
    Leg "1" --> "1..*" Journey: consist of
    

```