# Introduction

Public transportation systems are integral to urban mobility, facilitating the movement of millions of passengers daily.
The efficiency of these systems relies heavily on robust routing algorithms that optimize travel routes, minimize travel
times, and enhance the overall user experience. This thesis investigates the challenges associated with public transit
routing and explores innovative approaches to address these challenges.

## Motivation

This thesis is driven by several key challenges in public transit routing. In recent years, many public transit agencies
have begun publishing their schedules using the General Transit Feed Specification (GTFS) format as open data [3].
Maintaining accurate public transit schedules is a resource-intensive task. The sheer volume and complexity of
GTFS data present significant challenges for developing efficient data structures and processing methodologies.

Public transit routing is inherently complex due to the time-dependent nature of transit networks. Transit schedules
vary based on the time of day, day of the week, and other temporal factors, adding an additional layer of complexity to
the routing process. Developing efficient algorithms that account for this time-dependency remains a challenging task in
transportation research. Traditional graph-based routing algorithms often face performance issues when dealing with
large-scale transit networks, leading to very large graph structures and computational cost in preparing such graphs.
The RAPTOR (Round-based Public Transit Routing) algorithm, recognized for its speed and accuracy, offers a promising
solution to these performance limitations [4] as it can operate directly on the schedule information
and requires little pre-processing.

Developing a public transit routing system was found to be an optimal challenge as it integrates various aspects of the
Master of Advanced Studies in Software Engineering curriculum, including software architecture, algorithms and data
structures, automation, distributed systems communication, testing, and containerized deployment. This project adopts an
agile, iterative development methodology, providing an opportunity to address complex challenges while gaining practical
experience in software engineering.

## Research Questions

The primary research question addressed by this thesis is how the RAPTOR algorithm can be implemented and validated
within the context of the Swiss public transit network. This question is particularly relevant given the complexity and
scale of the network, which poses significant challenges for routing algorithms. A related research question focuses on
the optimization of the RAPTOR algorithm in Java and C++ and comparing the performance of both programming environments
for such a task.

These research questions are framed within the context of the current state of public transit networks. The complexity
of these networks, which involve multiple routes, stops, footpaths, and transfer points, necessitates the development of
routing algorithms that account for factors such as transfer times, service frequencies, and real-time constraints. The
research seeks to address these challenges while also considering scalability, as expanding transit systems further
complicates the problem space.

## Approach and Expected Outcomes

This thesis adopts a comprehensive approach to address the identified challenges, beginning with the utilization of GTFS
data as the foundation for the transit routing system. The standardized format of GTFS [3], which includes
static information such as stop times, routes, and trips, provides a consistent and reliable dataset for the
implementation of routing algorithms. A memory-efficient library for reading and processing GTFS schedules will be
developed to enable scalable management of large datasets, ensuring the system can handle large-scale transit networks
effectively.

One of the core aspects of this thesis is the implementation of the RAPTOR algorithm [4], which is
designed to efficiently compute transit routes by considering time dependencies such as schedules and transfer windows.
The RAPTOR algorithm employs a round-based approach, where transit routes are organized into discrete rounds, each
representing the number of trips needed. This structure simplifies the traversal of the network by enabling the
algorithm to explore transit options in rounds and return pareto-optimal solutions, minimizing both arrival time and the
number of transfers.

The system will be complemented with an integration layer that manages both the routing algorithm and the schedule,
while handling all necessary conversions between the two. This design maintains the independence of the schedule and the
routing algorithm, enabling a modular architecture. The modularity allows for system components to be modified or
replaced without affecting external dependencies, ensuring the system's adaptability and long-term maintainability.

To facilitate interaction with the system, a REST API will be developed, allowing external applications to access the
routing and scheduling services. This API will provide the foundation for seamless integration between the routing
algorithm and external systems. As a proof of concept, a simple web application will be created to visualize search
results and demonstrate the capabilities of the backend service. While the web application will serve as a proof of
concept, the primary focus of this thesis remains on developing the backend service.

This approach ensures the development of a scalable, high-performance public transit routing package based on the RAPTOR
algorithm, as well as a flexible service component capable of managing complex transit schedules and routes. The end
result is a modular system, complemented by a user-friendly interface that showcases the potential of the underlying
backend service.

## Scope and Delimitation

This thesis is carried out as part of a student project, with the primary objective of advancing knowledge and
methodologies related to public transit routing. There is no intention to develop a commercial product as part of this
work. All development and research activities are carried out as part of the Master of Advanced Studies in Software
Engineering program at the Eastern Switzerland University of Applied Sciences (OST), and no external company interests
influence the scope or outcomes of this research.
