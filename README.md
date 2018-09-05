# Telemetry
Telemetry collects runtime statistics from the Servers it is installed on, such
as CPU and RAM usage, Network utilization or other parameters. By default, the
statistics are collected every 10 seconds and sent to an Influxdb backend.

The data can then be used to display graphs and trigger alerts via Grafana.

# Monitoring Service

The monitoring service keeps track of all available and used system resources,
allowing us to spot bottlenecks, memory leaks and errors early. It is configured
to display all the data in a convenient web interface for easy access, and
reports once certain values exceed predefined thresholds.

It consists of three seperate services: the Data collector, time series database
and graphical frontend.

Other monitoring solutions that were validated include Nagios and Netdata And
Elasticsearch.

Nagios is complex to set up and not performant enough to log and graph multiple
metrics per minute. Netdata is not flexible enough, as it does not allow the
easy export of gathered data or the definition of own metrics.

### Data Collector
The data collection is done by a telemetry daemon running on the monitored
hosts. We are using [telegraf](https://github.com/influxdata/telegraf) for this
task. It's purpose is to collect all metrics defined in a config file, cache
them for a short amount of time and transfering them to the time series database
via a TCP or UDP network connection.

### Time series database
The time series database is responsible for storing all collected metrics for
each host, indexed by hostname, metric name, metric type and timestamp. We are
using [InfluxDB](https://github.com/influxdata/influxdb) for this purpose, since
it specialises on time-series data unlike competing products like PostgreSQL and
Elasticsearch, while being easier to setup and maintain than Prometheus. Other
feature of the time series database include the querying of the data, deletion
of old datasets, real time transformation of the data (such as integrals,
differentials, sums) etc.

### Graphical Frontend
The graphical Frontend is used to display the collected metrics, and allow the
user to build queries to retrieve data in a specialized fashion. We are using
[Grafana](https://github.com/grafana/grafana) for this. Its main purpose is
drawing graphs, but it also deals with rights management by prodviding a login
iterface. Also it offers the option to define Alarms on certain thresholds e.g.
System Load or Hard disk usage.

## Variables

```yml
# the telegraf version to use
telegraf_version: '1.5.1'
```

## Example Config
```yml
telegraph_version: '1.5.1'
```
