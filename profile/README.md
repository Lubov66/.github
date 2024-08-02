# VictoriaMetrics

VictoriaMetrics is a fast, cost-saving, and scalable solution for monitoring and managing time series data. It delivers high performance and reliability, making it an ideal choice for businesses of all sizes.

- Documentation: [docs.victoriametrics.com](https://docs.victoriametrics.com)
- Case studies: [Grammarly, Roblox, Wix,...](https://docs.victoriametrics.com/casestudies/).
- Available: [Binary releases](https://github.com/VictoriaMetrics/VictoriaMetrics/releases/latest), [Docker images](https://hub.docker.com/r/victoriametrics/victoria-metrics/), [Source code](https://github.com/VictoriaMetrics/VictoriaMetrics)
- Deployment types: [Single-node version](https://docs.victoriametrics.com/), [Cluster version](https://docs.victoriametrics.com/cluster-victoriametrics/), and [Enterprise version](https://docs.victoriametrics.com/enterprise/)
- Changelog: [CHANGELOG](https://docs.victoriametrics.com/changelog/), and [How to upgrade](#how-to-upgrade-victoriametrics)
- Community: [Slack](https://slack.victoriametrics.com/), [Twitter](https://twitter.com/VictoriaMetrics), [LinkedIn](https://www.linkedin.com/company/victoriametrics/), [YouTube](https://www.youtube.com/@VictoriaMetrics)

Yes, we open-source both the single-node VictoriaMetrics and the cluster version.

## Prominent features

VictoriaMetrics is optimized for timeseries data, even when old time series are constantly replaced by new ones at a high rate, it offers a lot of features:

* **Long-term storage for Prometheus** or as a drop-in replacement for Prometheus and Graphite in Grafana.
* **Powerful stream aggregation**: Can be used as a StatsD alternative.
* **Ideal for big data**: Works well with large amounts of time series data from APM, Kubernetes, IoT sensors, connected cars, industrial telemetry, financial data and various [Enterprise workloads](https://docs.victoriametrics.com/enterprise/).
* **Query language**: Supports both PromQL and the more performant MetricsQL.
* **Easy to setup**: No dependencies, single [small binary](https://medium.com/@valyala/stripping-dependency-bloat-in-victoriametrics-docker-image-983fb5912b0d), configuration through command-line flags, but the default is also fine-tuned; backup and restore with [instant snapshots](https://medium.com/@valyala/how-victoriametrics-makes-instant-snapshots-for-multi-terabyte-time-series-data-e1f3fb0e0282).
* **Global query view**: Multiple Prometheus instances or any other data sources may ingest data into VictoriaMetrics and queried via a single query.
* **Various Protocols**: Support metric scraping, ingestion and backfilling in various protocol.
    * [Prometheus exporters](#how-to-scrape-prometheus-exporters-such-as-node-exporter), [Prometheus remote write API](#prometheus-setup), [Prometheus exposition format](#how-to-import-data-in-prometheus-exposition-format).
    * [InfluxDB line protocol](#how-to-send-data-from-influxdb-compatible-agents-such-as-telegraf) over HTTP, TCP and UDP.
    * [Graphite plaintext protocol](#how-to-send-data-from-graphite-compatible-agents-such-as-statsd) with [tags](https://graphite.readthedocs.io/en/latest/tags.html#carbon).
    * [OpenTSDB put message](#sending-data-via-telnet-put-protocol).
    * [HTTP OpenTSDB /api/put requests](#sending-opentsdb-data-via-http-apiput-requests).
    * [JSON line format](#how-to-import-data-in-json-line-format).
    * [Arbitrary CSV data](#how-to-import-csv-data).
    * [Native binary format](#how-to-import-data-in-native-format).
    * [DataDog agent or DogStatsD](#how-to-send-data-from-datadog-agent).
    * [NewRelic infrastructure agent](#how-to-send-data-from-newrelic-agent).
    * [OpenTelemetry metrics format](#sending-data-via-opentelemetry).
* **NFS-based storages**: Supports storing data on NFS-based storages such as Amazon EFS, Google Filestore.
* And many other features such as metrics relabeling, cardinality limiter, etc.

## Benchmarks 

Some good benchmarks VictoriaMetrics achieved:

* **Minimal memory footprint**: handling millions of unique timeseries with [10x less RAM](https://medium.com/@valyala/insert-benchmarks-with-inch-influxdb-vs-victoriametrics-e31a41ae2893) than InfluxDB, up to [7x less RAM](https://valyala.medium.com/prometheus-vs-victoriametrics-benchmark-on-node-exporter-metrics-4ca29c75590f) than Prometheus, Thanos or Cortex.
* **Highly scalable and performance** for [data ingestion](https://medium.com/@valyala/high-cardinality-tsdb-benchmarks-victoriametrics-vs-timescaledb-vs-influxdb-13e6ee64dd6b) and [querying](https://medium.com/@valyala/when-size-matters-benchmarking-victoriametrics-vs-timescale-and-influxdb-6035811952d4), [20x outperforms](https://medium.com/@valyala/insert-benchmarks-with-inch-influxdb-vs-victoriametrics-e31a41ae2893) InfluxDB and TimescaleDB.
* **High data compression**: [70x more data points](https://medium.com/@valyala/when-size-matters-benchmarking-victoriametrics-vs-timescale-and-influxdb-6035811952d4) may be stored into limited storage than TimescaleDB, [7x less storage](https://valyala.medium.com/prometheus-vs-victoriametrics-benchmark-on-node-exporter-metrics-4ca29c75590f) space is required than Prometheus, Thanos or Cortex.
* **Reducing storage costs**: [10x more effective](https://docs.victoriametrics.com/casestudies/#grammarly) than Graphite according to the Grammarly case study.
* **A single-node VictoriaMetrics** can replace medium-sized clusters built with competing solutions such as Thanos, M3DB, Cortex, InfluxDB or TimescaleDB. See [VictoriaMetrics vs Thanos](https://medium.com/@valyala/comparing-thanos-to-victoriametrics-cluster-b193bea1683), [Measuring vertical scalability](https://medium.com/@valyala/measuring-vertical-scalability-for-time-series-databases-in-google-cloud-92550d78d8ae), [Remote write storage wars - PromCon 2019](https://promcon.io/2019-munich/talks/remote-write-storage-wars/).
* **Optimized for storage**: [Works well with high-latency IO](https://medium.com/@valyala/high-cardinality-tsdb-benchmarks-victoriametrics-vs-timescaledb-vs-influxdb-13e6ee64dd6b) and low IOPS (HDD and network storage in AWS, Google Cloud, Microsoft Azure, etc.).

## Community and contributions

Feel free asking any questions regarding VictoriaMetrics:

* [Slack Inviter](https://slack.victoriametrics.com/) and [Slack channel](https://victoriametrics.slack.com/)
* [Twitter](https://twitter.com/VictoriaMetrics/)
* [Linkedin](https://www.linkedin.com/company/victoriametrics/)
* [Reddit](https://www.reddit.com/r/VictoriaMetrics/)
* [Telegram-en](https://t.me/VictoriaMetrics_en)
* [Telegram-ru](https://t.me/VictoriaMetrics_ru1)
* [Google groups](https://groups.google.com/forum/#!forum/victorametrics-users)
* [Mastodon](https://mastodon.social/@victoriametrics/)

If you like VictoriaMetrics and want to contribute, then please [read these docs](https://docs.victoriametrics.com/contributing/).