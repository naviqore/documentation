# RAPTOR

The **RAPTOR** (Round-based Public Transit Routing) algorithm is a powerful algorithm to compute optimal routes in
public transportation systems, especially for large and complex networks. Its primary objective is to efficiently
determine the best route options based on factors like arrival time and number of transfers. RAPTOR is particularly
useful for real-time journey planning due to its speed and adaptability.

### Key Concepts of RAPTOR:

- **Initialization**: The algorithm starts at the origin station and time specified by the user. Initially, it only
  considers the starting station, marking it for the first round of exploration.

- **Round-based Search**: The search process is broken into several rounds. In each round, the algorithm evaluates all
  transport lines connected to the current list of stations. It computes the earliest possible arrival times at the
  stations along each line and adds them to the list of stations for the next round.

- **Updating Arrival Times**: As the algorithm processes new stations, it updates their earliest arrival times. If it
  finds a route to a station that is faster than the previously known route, the arrival time and corresponding route
  are updated.

- **Termination Condition**: The algorithm stops when it reaches the destination station with the optimal arrival time
  or when no further improvements can be made after a set number of rounds.

- **Tracing the Optimal Route**: Once the algorithm concludes, the optimal route is reconstructed by tracing the updated
  arrival times back from the destination to the start station.

RAPTOR is highly efficient because it operates directly on schedule information without the need to build extensive
graphs that incorporate the complexity of transfers. This characteristic makes RAPTOR particularly suitable for
networks of any size, as it avoids the need for time-consuming preprocessing. This efficiency allows us to enable
features like accessibility and bike information on our routes.

## Sequence Diagram RAPTOR (simplified)

```mermaid
sequenceDiagram
  participant Algorithm
  participant Stops
  participant Routes
  participant Trips
  participant FootPaths
  Algorithm ->> Stops: Initialize and mark start stop

  loop Main iterations (k)
    Algorithm ->> Stops: Identify marked stops
    Stops ->> Routes: Get routes serving marked stops
    Routes ->> Trips: Traverse routes and trips

    alt Can update stops?
      Trips ->> Stops: Update stop times and mark new stops
    end

    Algorithm ->> FootPaths: Check foot-path connections
    FootPaths ->> Stops: Update stops via foot-paths

    alt No stops updated
      Algorithm ->> Algorithm: Stop process
    end
  end

```

- The algorithm starts at the departure stop at the given departure time. It initializes a list of stops to visit in
  this round (initially just the departure stop), and a list of already visited stops.
- The algorithm performs several "rounds" of search. In each round, it considers all transit lines that stop at the
  stops in the current round. For each line, it calculates the earliest arrival time at each stop along the line that
  hasn't been visited yet, and adds these stops to the list for the next round.
- When the algorithm finds a new stop, it updates the earliest arrival time at this stop. If the new arrival time is
  earlier than the previous one, it updates the route.
- After the algorithm has terminated, the optimal route can be found by backtracking the updated arrival times from the
  destination stop to the departure stop.

## Elements of the Raptor algorithm

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

![chap2-public-transit.pdf](raptor-timetable.png){width="650"}

##### Stops

![chap2-public-transit.pdf](raptor-stops.png){width="650"}

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

![chap2-public-transit.pdf](raptor-connection.png){width="650"}

#### Trip

- Sequence of connections

```tex
T = (c_{1} , . . . , c_{k} )
```

- Represents a single vehicle
- driving from first to last stop
- at specific times

![chap2-public-transit.pdf](raptor-trip1.png){width="650"}

![chap2-public-transit.pdf](raptor-trip2.png){width="650"}

#### Route

In the context of the RAPTOR algorithm, a **Route** refers to:

- **Definition**: A sequence of trips that share the same sequence of stops.
- **Function**: Vehicles like buses or trains follow these predefined lines to pick up and drop off passengers at each
  stop.
- **Usage**: The RAPTOR algorithm processes each route to compute arrival times and determine the fastest journey with a
  limited number of transfers.
- **Optimization**: Routes are scanned efficiently, with the algorithm looking at each route at most once per round,
  contributing to RAPTOR's speed and dynamic capabilities.

![chap2-public-transit.pdf](raptor-route.png){width="650"}

## The RAPTOR Algorithm Explained in Detail

### Key Features of RAPTOR

**Pareto-Optimality:** RAPTOR computes Pareto-optimal connections, meaning it considers multiple criteria, such as
earliest arrival time and the fewest transfers. A connection is Pareto-optimal if no objective (number of transfers or
arrival time) can be improved without worsening the other.

**Round-based Processing:** The algorithm processes journeys in rounds, where each round computes the arrival times for
journeys that use a specific number of transfers.

**Efficient Route Scanning:** RAPTOR explicitly uses the structure of public transit timetables, scanning each transit
route
at most once per round. This ensures that the algorithm is fast and scalable, even for large transit networks.

### How RAPTOR Works

**Initialization:**
Given a source stop s, a target stop t, and a departure time τ_dep, the algorithm initializes the journey from s.

**Rounds:**
Each round k computes all journeys with exactly k trips. In the first round, RAPTOR computes journeys with no transfers,
i.e., direct trips. In subsequent rounds, it computes journeys with one transfer, two transfers, and so on.

![chap2-public-transit.pdf](raptor-rounds.png){width="650"}

**Route Scanning:**
For each round, the algorithm scans all stops from routes passing through stops marked in the previous round. At each
stop, it checks whether the current trip (if already on a trip) reduces the arrival time at that stop and boards the
earliest available trip departing from the stop, provided the stop was marked in the previous round or already on a
trip.

![chap2-public-transit.pdf](raptor-scan.png){width="650"}

![chap2-public-transit.pdf](route-scan2.png){width="650"}

**Stopping Condition:**
The algorithm terminates when no further improvements in arrival times are possible, ensuring it only performs the
necessary number of rounds.

### Conclusion

RAPTOR's design makes it suitable for real-time, interactive journey planning, where users may need fast responses to
queries about optimal public transit routes. The algorithm can also be extended to handle additional criteria like fare
zones or transfer reliability, making it highly adaptable to different transit systems.
One of RAPTOR's strengths is its flexibility, allowing it to be extended to handle additional constraints beyond arrival
time and number of transfers. This extended version is called Multi-Constraint RAPTOR (McRAPTOR). McRAPTOR can optimize
multiple criteria simultaneously, such as minimizing travel through fare zones, increasing transfer reliability, or
incorporating user preferences like minimizing walking distances or choosing specific transit lines.

Unlike RAPTOR, which focuses solely on minimizing time and transfers, McRAPTOR maintains Pareto-optimal sets of
journeys, considering all relevant criteria. This means that McRAPTOR returns a set of non-dominated journeys—where no
journey is worse than another in all criteria. Each stop is associated with a set of labels, where each label represents
a journey's costs for different metrics (e.g., time, fare zones). The algorithm iterates through the network, updating
these labels and discarding any dominated (non-optimal) journeys.

However, **McRAPTOR was not implemented** as part of this project, which focused on the base RAPTOR algorithm to prioritize
speed and simplicity in optimizing arrival times and transfers.