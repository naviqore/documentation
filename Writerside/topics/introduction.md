# Introduction

Public transportation systems are integral to urban mobility, facilitating the movement of millions of passengers daily.
The efficiency of these systems relies heavily on robust routing algorithms that optimize travel routes, minimize travel
times, and enhance the overall user experience. This thesis investigates the challenges associated with public transit
routing and explores innovative approaches to address these challenges.

## Motivation

This thesis is driven by several key challenges in public transit routing. In recent years, many public transit agencies
have begun publishing their schedules using the General Transit Feed Specification (GTFS) format as open data [3].
Maintaining accurate public transit schedules is a resource-intensive task. The volume and complexity of
GTFS data present significant challenges for developing efficient data structures and processing methodologies.

Public transit routing is inherently complex due to the time-dependent nature of transit networks. Transit schedules
vary based on the time of day, day of the week, and service exceptions for specific dates, adding a layer of complexity
to the routing process. Developing efficient algorithms that account for this time-dependency remains a challenging task
in transportation research. Traditional graph-based routing algorithms often face performance issues when dealing with
large-scale transit networks, leading to very large graph structures and computational cost in preparing such graphs.
The RAPTOR (**R**ound-b**A**sed **P**ublic **T**ransit **O**ptimized **R**outer) algorithm, recognized for its speed and
accuracy, offers a promising solution to these performance limitations [4] as it can operate directly on the schedule
information and requires little pre-processing.

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
research seeks to address these challenges.

## Approach and Expected Outcomes

To address the identified challenges, a comprehensive approach was defined, beginning with the utilization of GTFS
data [3] as the foundation for the transit routing system. A memory-efficient library for reading and processing
GTFS schedules will be developed to enable scalable management of large datasets, ensuring the system can handle
large-scale transit networks effectively.

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

## Scope and Delimitation

This thesis is part of the Master of Advanced Studies in Software Engineering at the Eastern Switzerland University of
Applied Sciences (OST). It focuses on applying the knowledge gained from the program to further advance methodologies in
public transit routing, with no external company interests influencing the scope or outcomes of this research.