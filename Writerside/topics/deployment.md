# Deployment

Deployment of the complete Naviqore system, which consists of a public transit service based on GTFS and the extended
Raptor algorithm, along with a simple viewer.

## Configuration

The configuration of the public transit service is best handled through environment variables. This approach
provides flexibility and allows for easier management across different environments, such as development, and
production. Below are some of the key environment variables that are essential for configuring the router:

- **GTFS_STATIC_URI**: URL or file path to a static GTFS feed. The service will initially fetch the GTFS from this URL.
  If the provided value is a file path, the GTFS is loaded from the file and the update interval is ignored.
  Example for Switzerland: `https://opentransportdata.swiss/en/dataset/timetable-2024-gtfs2020/permalink`

- **GTFS_STATIC_UPDATE_CRON**: Cron expression for updating the static GTFS feed from the provided URL. Public transit
  agencies update their static GTFS data regularly. Set this interval to match the agency's publish schedule. Default is
  to update the schedule daily at 4 AM.

- **TRANSFER_TIME_SAME_STOP_DEFAULT**: Default transfer time between same stop transfers in seconds. If GTFS already
  provides same stop transfer times, those have precedence over this default. If the value is set to 0, no additional
  same stop transfer times are set.

- **TRANSFER_TIME_BETWEEN_STOPS_MINIMUM**: Minimum transfer time between the different stops in seconds. If stops are
  closer than this, this time has precedence over the actual walking time, which accounts for leaving the station
  building, stairways, etc. If GTFS already provides a transfer time between two stops, the GTFS time has precedence
  over this minimum. If the value is set to -1, no additional transfers will be created.

- **TRANSFER_TIME_ACCESS_EGRESS**: Time in seconds required to access or egress from a public transit trip. This time is
  added twice to the walking duration of transfers between two stops and once to first and last mile walking legs.

- **WALKING_SEARCH_RADIUS**: Search radius in meters. No walks with a longer beeline distance between origin and
  destination will appear in connections (first/last mile and between stop transfers). The actual distance of the walk
  might be longer. Note: This radius is also used to generate same stop transfers.

- **WALKING_SPEED**: Walking speed in meters per second. The default value is based on the average preferred walking
  speed.

- **WALKING_DURATION_MINIMUM**: Minimum walking duration in seconds. If the walking duration, without access or egress
  time (see 'TRANSFER_TIME_ACCESS_EGRESS'), is shorter, no first or last mile walk is needed to reach the location. This
  avoids very short walks inside stations that give a false sense of accuracy.

- **RAPTOR_DAYS_TO_SCAN**: Number of dates surrounding the queried date should be included in the scan. This is useful
  if the previous GTFS service day includes trips on the queried date. Or the connection is so long that it continues
  into the next service day. The default value is 3, which includes the previous, current, and next service day.

- **RAPTOR_RANGE**: Maximum range in seconds to identify departures or arrivals for scanning in order to reduce the
  travel time (a.k.a. range Raptor). Values smaller than 1 are allowed and imply using the standard Raptor algorithm.
  The default value is -1, which means no range.

For further configuration settings, such as those related to caching, logging, and application management, please refer
directly to
the [application.properties](https://github.com/naviqore/public-transit-service/blob/main/src/main/resources/application.properties)
file.

## Helm Chart

This [Helm chart](https://github.com/naviqore/deployment) defines the Kubernetes resources required to deploy the
service and viewer in the cloud. The public transit service can be configured by overriding the default environment
variables via Helm's values mechanism.

## Docker Compose

This [Docker Compose](https://github.com/naviqore/deployment/blob/main/docker-compose.yml) setup provides an alternative
method to deploy the service and viewer, particularly suited for local development. To configure the routing service,
the environment variables should be adjusted within the Docker Compose file.
