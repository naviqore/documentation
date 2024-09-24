# GTFS

General Transit Feed Specification (GTFS), is a standardized data format used for sharing public transportation
schedules and related geographic information. It was originally developed by Google in partnership with the public
transportation agency TriMet, to enable public transit agencies to publish their data in a format that is easily
consumed by applications like Google Maps, making public transit data more accessible and useful for riders.

## Key Components of GTFS

GTFS consists of a series of text files stored in a ZIP archive, each containing specific information about different
aspects of a public transit network. These files define various entities, such as **stops.txt** for station locations, *
*routes.txt** for transit routes, and **trips.txt** for individual trips along those routes. Figure 1 presents the
domain model for GTFS files provided by the Open Data Platform Mobility Switzerland [1], illustrating how the fields in
each file interact to form a cohesive public transport network. While this example does not cover all GTFS files or
fields, it offers a clear overview of the most essential components. For a complete list of GTFS files and their fields,
refer to the official GTFS reference [2].

## Usage of GTFS

GTFS data is used in various ways to enhance public transit systems and improve user experience. **Public transit apps**
like Google Maps and Apple Maps use GTFS feeds for route planning, schedule information, and real-time transit updates.
**Transit agencies** utilize GTFS for scheduling, route optimization, and operational analysis. **Data analysts and
urban planners** rely on GTFS for performance analysis, accessibility studies, and transit network modeling. *
*Information systems** at stations and stops leverage GTFS data to display real-time arrival and departure information,
route details, and service updates.

## File Format - Example

**routes.txt**:

````text
route_id,agency_id,route_short_name,route_long_name,route_desc,route_type
"91-10-A-j22-1","37","10","","T","900"
"91-10-B-j22-1","78","S10","","S","109"
"91-10-C-j22-1","11","S10","","S","109"
"91-10-E-j22-1","65","S10","","S","109"
"91-10-F-j22-1","11","RE10","","RE","106"
"91-10-G-j22-1","11","SN10","","SN","109"
"91-10-j22-1","3849","10","","T","900"
"91-10-Y-j22-1","82","IR","","IR","103"3
````

The diagram below illustrates how the different types of information interact.

![gtfs_object_diagram.png](https://opentransportdata.swiss/wp-content/uploads/2016/11/gtfs_static.png)
