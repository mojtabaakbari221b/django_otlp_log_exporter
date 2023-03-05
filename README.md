# django otlp log exporter (handler)

## Collecting Logs using OpenTelemetry

OpenTelemetry provides various receivers and processors for collecting first-party and third-party logs directly via OpenTelemetry Collector or via existing agents such as FluentBit so that minimal changes are required to move to OpenTelemetry for logs.

## Collecting legacy first-party Application Logs

There are two ways to collect logs from these applications.

### Via File or Stdout Logs

Here, the logs of the application are directly collected by the OpenTelemetry receiver using collectors like filelog receiver and operators and processors to parse them into the OTel model.

### Direct to collector ( our handler is implemented based on this approach )

In this approach you can modify your logging library that is used by the application to use the logging SDK provided by OpenTelemetry and directly forward the logs from the application to OpenTelemetry. This approach removes any need for agents/intermediary medium but loses the simplicity of having the log file locally.

![https://github.com/mojtabaakbari221b/django_otlp_log_exporter/blob/main/direct_to_collector.png](https://github.com/mojtabaakbari221b/django_otlp_log_exporter/blob/main/direct_to_collector.png)

## Our Approach

You can directly send your application logs to your opentelementry collector with our log handler (which is finally delivered to backends like signoz.)

## Installation

```python
pip install django-otlp-log-exporter
```

## Configuration (settings.py)

```python
OTLP_ENDPOINT = env('OTLP_ENDPOINT') # its endpoint of your opentelementry collector listen on
OTLP_IS_SECURE = env('OTLP_IS_SECURE') # its bool
```

```python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'directlogging': {
            'level': 'WARNING',
            'class': 'otlp_exporter.handler.DirectWriteLoggingHandler',
        },
    },
    'loggers': {
        'root': {
            'handlers': [
                'directlogging',
            ],
            'level': 'WARNING',
            'propagate': True,
        },
    },
}
```

#### Links:
Much of our documentation is based on signoz.io's descriptions.

Thanks for the inspirations of other packages written, especially https://github.com/jayfk/django-fluentd . If you find a bug or have a question, you can contact me via the link below mojtaba.akbari.221B@gmail.com.
