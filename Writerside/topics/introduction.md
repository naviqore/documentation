# Introduction to Public Transit Routing with RAPTOR Algorithm

# Introduction

Public transportation systems play a crucial role in urban mobility, connecting millions of people daily. Efficient
routing algorithms are essential for optimizing transit journeys, minimizing travel time, and enhancing user experience.
In this Master thesis, we delve into the challenges of public transit routing and explore innovative approaches to
address them.

## Motivation

The motivation behind our research lies in addressing several key challenges:

1. **Efficiency**: Traditional transit routing algorithms often struggle with large-scale networks, resulting in
   suboptimal routes and longer travel times. The RAPTOR algorithm, known for its speed and accuracy, offers a promising
   solution.

2. **Real-Time Updates**: Incorporating real-time data—such as delays, service disruptions, and vehicle positions—allows
   us to provide dynamic routing recommendations. By integrating live feeds from transit agencies, we aim to enhance the
   reliability of our system.

3. **User-Friendly Interfaces**: We recognize the importance of user-friendly interfaces for both technical experts and
   everyday commuters. Our application will cater to diverse user groups, from data scientists to casual travelers.

## Approach

Our approach involves the following key components:

1. **Data Source**: We utilize the General Transit Feed Specification (GTFS) data for Switzerland. GTFS provides a
   standardized format for transit schedules, including static information (such as stop times, routes, and trips) and
   real-time updates.

2. **RAPTOR Algorithm**: The RAPTOR algorithm, based on time-expanded networks, efficiently computes transit routes by
   considering time-dependent constraints. We will adapt and optimize this algorithm for Swiss transit networks.

3. **Web Application**: Around the core routing functionality, we develop a web application. The frontend will allow
   users to explore schedules, query connections, and assess accessibility. The backend continuously updates the
   schedule using live feeds. WOLLEN WIR DAS WIRKLICH HIER AUFFÜHREN?

## Research Questions

Our research aims to address the following questions:

1. How can we enhance the RAPTOR algorithm for Swiss transit networks?
2. What user interface features are essential for both technical users and everyday commuters?
3. How can we seamlessly integrate real-time data into our routing system?

## Expected Outcomes

By the end of this thesis, we anticipate achieving the following outcomes:

1. A performant public transit router based on the RAPTOR algorithm.
2. A user-friendly web application that empowers users to explore transit schedules, plan routes, and assess
   accessibility.
3. Insights into the challenges and opportunities of integrating real-time data into transit routing systems.

Our work contributes to the field of transportation planning and provides practical tools for improving public transit
experiences. 🚆🌐

## Initial situation


## Background

The existing literature highlights several complexities associated with transit routing:

1. **Network Complexity**: Public transit networks are intricate, with multiple routes, stops, and interconnections.
   Finding optimal paths requires considering various factors such as transfer times, waiting times, and service
   frequencies.

2. **Real-Time Constraints**: Passengers expect real-time information on transit availability and delays. Incorporating
   live data into routing algorithms is essential for accurate predictions.

3. **Scalability**: As cities grow, transit networks expand, leading to scalability challenges. Traditional algorithms
   struggle to handle large-scale networks efficiently.

## Round-Based Approach

Our research builds upon the groundbreaking work presented in the "Round-Based Public Transit Routing" paper by
Microsoft. This paper introduces a novel approach that organizes transit routes into rounds, simplifying the routing
process. Each round represents a set of interconnected trips, allowing for efficient traversal through the network.


## Thesis

## Delimitation
