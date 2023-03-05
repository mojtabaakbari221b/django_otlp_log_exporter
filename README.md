# django otlp log exporter (handler)

## Collecting Logs in SigNoz using OpenTelemetry

OpenTelemetry provides various receivers and processors for collecting first-party and third-party logs directly via OpenTelemetry Collector or via existing agents such as FluentBit so that minimal changes are required to move to OpenTelemetry for logs.

## Collecting legacy first-party Application Logs

There are two ways to collect logs from these applications.

### Via File or Stdout Logs

Here, the logs of the application are directly collected by the OpenTelemetry receiver using collectors like filelog receiver and operators and processors to parse them into the OTel model.

### Direct to collector ( our handler is implemented based on this approach )

In this approach you can modify your logging library that is used by the application to use the logging SDK provided by OpenTelemetry and directly forward the logs from the application to OpenTelemetry. This approach removes any need for agents/intermediary medium but loses the simplicity of having the log file locally.

![alt text](https://github.com/mojtabaakbari221b/django_otlp_log_exporter/blob/main/direct_to_collector.png)
