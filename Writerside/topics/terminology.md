# Terminology

## Definition of the individual elements of the Raptor algorithm

### In the context of public transit systems, the following terms are essential:

#### Timetable

- Set S: This is the **collection of stops**, which includes all train stations, platforms, bus stops, and similar
  locations
  where passengers can board or disembark from transit vehicles.
- Set C: This represents the **elementary connections** within the transit network, linking the stops in Set S and
  defining
  the possible routes for trips.
- Set T: This **comprises all trips** made by transit vehicles such as trains, buses, and trams. Each trip follows a
  specific sequence of stops from Set S, connected through the elementary connections in Set C.

##### Network

![raptor-timetable.png](raptor-timetable.png)

##### Stops

![raptor-stops.png](raptor-stops.png)

##### Connection

A connection is represented as a 5-tuple:

```tex
c = (v_{dep}(c), v_{arr}(c), \tau_{dep}(c), \tau_{arr}(c), trip(c))
```

V = Vertex (represents a stop from the set S)

- **Departure stop**:

```tex 
- v_{dep}(c) \in S
```

departure stop of the connection c is an element of the set S of stops

- **Arrival stop**:

```tex
v_{arr}(c) \in S
```

- **Trip**:

```tex
trip(c) \in T
```

Example connection times:

- **Departure time**:

```tex
\tau_{dep}(c): 8:00
```

- **Arrival time**:

```tex
\tau_{arr}(c): 8:30
```

![raptor-connection.png](raptor-connection.png)

#### Trip

- Sequence of connections

```tex
T = (c_{1} , . . . , c_{k} )
```

- Represents a single vehicle
- driving from first to last stop
- at specific times

![raptor-trip1.png](raptor-trip1.png)

![raptor-trip2.png](raptor-trip2.png)

#### Route

In the context of the RAPTOR algorithm, a **Route** refers to:

- **Definition**: A sequence of trips that share the same sequence of stops.
- **Function**: Vehicles like buses or trains follow these predefined lines to pick up and drop off passengers at each
  stop.
- **Usage**: The RAPTOR algorithm processes each route to compute arrival times and determine the fastest journey with a
  limited number of transfers.
- **Optimization**: Routes are scanned efficiently, with the algorithm looking at each route at most once per round,
  contributing to RAPTOR's speed and dynamic capabilities.

![raptor-route.png](raptor-route.png)