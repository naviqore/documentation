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

### stop_times.txt
```text

trip_id,arrival_time,departure_time,stop_id,stop_sequence,pickup_type,drop_off_type
"1.TA.1-9-j17-1.1.H","05:25:00","05:25:00","8502034:0:2","1","0","0"
"1.TA.1-9-j17-1.1.H","05:28:00","05:29:00","8502033:0:2","2","0","0"
"1.TA.1-9-j17-1.1.H","05:33:00","05:33:00","8502032:0:1","3","0","0"
"1.TA.1-9-j17-1.1.H","05:36:00","05:36:00","8502031:0:1","4","0","0"
"1.TA.1-9-j17-1.1.H","05:42:00","05:42:00","8502030:0:2","5","0","0"
"1.TA.1-9-j17-1.1.H","05:50:00","05:50:00","8502119:0:7","6","0","0"
"2.TA.1-9-j17-1.2.H","05:53:00","05:53:00","8502034:0:1","1","0","0"
"2.TA.1-9-j17-1.2.H","05:57:00","05:58:00","8502033:0:2","2","0","0"
"2.TA.1-9-j17-1.2.H","06:02:00","06:02:00","8502032:0:1","3","0","0"
"2.TA.1-9-j17-1.2.H","06:04:00","06:04:00","8502031:0:1","4","0","0"
"2.TA.1-9-j17-1.2.H","06:09:00","06:11:00","8502030:0:2","5","0","0"
```

### Technical description

The diagram below illustrates how the different types of information interact.

![gtfs_object_diagram.png](https://opentransportdata.swiss/wp-content/uploads/2016/11/gtfs_static.png){width="750"}


[1]: https://opentransportdata.swiss/en/cookbook/gtfs/
