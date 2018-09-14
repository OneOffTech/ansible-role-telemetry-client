Telemetry Client
================

Telemetry collects runtime statistics from the Servers it is installed on, such
as CPU and RAM usage, Network utilization or other parameters. By default, the
statistics are collected every 10 seconds and sent to an Influxdb backend.

The data can then be used to display graphs and trigger alerts via Grafana.


The data collection is done by a telemetry daemon running on the monitored
hosts. We are using [telegraf](https://github.com/influxdata/telegraf) for this
task. It's purpose is to collect all metrics defined in a config file, cache
them for a short amount of time and transfering them to the time series database
via a TCP or UDP network connection.

Requirements
------------

* A telemetry server has to be set up and running on a host, to take the
  telemetry data. This can be done using the Telemetry server role.

Role Variables
--------------

```yml
# the telegraf version to use
telegraf_version: '1.5.3'

# address to report to
telegraf_url: ''

# credentials to use for reporting (write-only)
telegraf_user: 'agent'
telegraf_password: 'changeme'
```

Example Configuration
---------------------

```yml
telegraf_version: "1.5.3"

telegraf_url: "http://monitoring.example.org:8086"
telegraf_user: "agent"
telegraf_password: "s3cur3"
```

Dependencies
------------

None


License
-------

MIT
