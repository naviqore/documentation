# Abstract

**Efficient Public Transit Routing with RAPTOR: A Production-Ready Solution Leveraging GTFS Data**

Timetable queries in public transportation present a complex problem. Traditional graph-based methods encounter their
limitations, especially when it comes to correctly representing transfers between different routes. The temporal
complexity of transfers makes a trivial representation nearly impossible. A promising alternative to these traditional
approaches is the Round-Based Public Transit Routing (RAPTOR) algorithm, developed by a team of Microsoft engineers in
collaboration with the Karlsruher Institute for Technology (KIT). This round-based algorithm does not require
conventional graph construction and operates directly on timetable data. Starting from the departure location, the
departures of all routes passing through are scanned. In subsequent rounds, all routes from stops newly reached in the
previous round are considered, until the destination is reached.

The goal of our work was to develop our own implementation of this algorithm and to use it with timetables based on the
General Transit Feed Specification (GTFS). The results of our work can be divided into two main areas:

1. Productive use of the RAPTOR algorithm: We extended the RAPTOR algorithm in our work so that it can be used in
   every day, productive systems. The algorithm was supplemented with features such as the ability to prioritize routes
   by departure or arrival times, and to define arbitrary query criteria (e.g., type of transportation, number of
   transfers, maximum walking distance, minimum transfer time, accessibility, or the ability to bring a bicycle). This
   extended version of the ”productive” RAPTOR algorithm was integrated into a Spring application with REST API,
   allowing it to be used by a web application.
2. Performance optimization: Another aspect of our work focused on performance optimization. We compared different
   implementations of the RAPTOR algorithm: the ”basic” RAPTOR, as proposed in the original paper, once in Java and once
   in C++.In addition, we investigated other implementations, such as the Multi-Day RAPTOR we developed, which enables
   scanning timetables over multiple service days, as well as Range RAPTOR, which was also described in the original
   RAPTOR paper.

Both aspects of our work were successfully implemented and contribute to advancing the RAPTOR algorithm both in theory
and practice.

**Keywords**: RAPTOR algorithm, GTFS, timetable routing, isolines routing, performance, optimization, public
transportation

**Authors**: Michael Brunner, Lukas Connolly, Merlin Unterfinger

## Acknowledgments

We would like to express our sincere gratitude to our supervisor, Thomas Letsch, for his invaluable guidance, insightful
feedback, and continuous support throughout this project. His expertise and encouragement were instrumental in shaping
the direction of our work.

Additionally, we extend our thanks to the Eastern Switzerland University of Applied Sciences and its dedicated lecturers
for providing us with the resources and learning environment that made this project possible. We also want to
acknowledge the open-source community, whose contributions to the development of tools and libraries played a
significant role in the success of our project.

Finally, we are deeply grateful to our friends and families for their unwavering support and understanding during the
long hours and late nights spent on this thesis. Without their patience and encouragement, this work would not have been
possible.
