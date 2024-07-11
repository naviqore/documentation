# GTFS

GTFS, or General Transit Feed Specification, is a standardized data format used for sharing public transportation
schedules and related geographic information. It was originally developed by Google in partnership with the public
transportation agency TriMet, to enable public transit agencies to publish their data in a format
that is easily consumed by applications like Google Maps, making public transit data more accessible and useful for
riders.

#### Key Components of GTFS

GTFS consists of a series of text files collected in a ZIP archive. Each file contains specific types of information
about the transit system, and these files are typically:

**agency.txt**:
Contains information about the transit agencies responsible for the data, including the agency name, URL,
and timezone.

**stops.txt**:
Lists all the stops where passengers can board or leave the transit vehicles. Each stop has details such as
stop ID, name, latitude, longitude, and possibly a description.

**routes.txt:**
Describes the routes that transit vehicles travel on, including route ID, short name, long name, and type of
transportation (bus, subway, etc.).

**trips.txt:**
Contains information about individual trips along the routes, such as trip ID, route ID, service ID, and trip
headsign.

**stop_times.txt:**
Provides the scheduled times that transit vehicles arrive at and depart from each stop along a trip.
This includes stop ID, trip ID, arrival time, and departure time.

**calendar.txt:**
Defines the service dates and days of the week that service is available, linking to specific trips.

**calendar_dates.txt:**
Lists exceptions to the standard schedule defined in the calendar.txt, such as holidays or special
service days.

**fare_attributes.txt:**
Describes the fare structure for the transit services, including fare prices, payment methods, and
transfer rules.

**fare_rules.txt:**
Defines the rules for applying fares to different routes, zones, and user categories.

**shapes.txt:**
Contains the actual geographic paths that the transit vehicles follow, described by sequences of latitude
and longitude points.

**frequencies.txt:**
Specifies headway (time between trips) for routes that run at regular intervals.

**transfers.txt:**
Details rules for transferring between routes, including transfer points and minimum transfer times.

**feed_info.txt:**
Provides metadata about the feed, such as the feed publisher, version, and the feed's start and end
dates.

[GTFS][1].

### Usage of GTFS

GTFS data is utilized in various ways to improve public transit systems and user experience:

**Public Transit Apps:**
GTFS data feeds are consumed by applications like Google Maps, Apple Maps, and other transit apps
to provide route planning, schedules, and real-time transit information.

**Transit Agency Tools:**
Transit agencies use GTFS data for planning and operations, helping them manage schedules,
optimize routes, and analyze performance.

**Data Analysis:**
Researchers and urban planners use GTFS data to analyze transit system performance, accessibility, and to
model changes in transit networks.

**Information Systems:**
Transit information systems at stations and stops use GTFS data to display arrival times, route
information, and service updates.

### File Format - Example

#### routes.txt

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

### Technical description

The diagram below illustrates how the different types of information interact.

![gtfs_object_diagram.png](https://opentransportdata.swiss/wp-content/uploads/2016/11/gtfs_static.png)


[1]: https://opentransportdata.swiss/en/cookbook/gtfs/
