This exporter is a Python server that connects to AWS Cost Explorer with a customizable period, and exposes last responses as Prometheus metrics. It gets the metrics from the AWS Cost Explorer API (0.01$ per request).

The code is mostly from Nacho Millan Garcias Git (Nadia found it). with some minor changes.(https://github.com/nachomillangarcia/prometheus_aws_cost_exporter)

The default Query period is set to 1800s (30 min).

The Configuration for Grafana:

| Metrics | Graphana |
| ------------- |:-------------:|
| METRIC_TODAY_DAILY_COSTS      | Enable aws_today_daily_costs metric      |
| METRIC_YESTERDAY_DAILY_COSTS | Enable aws_yesterday_daily_costs metric      |
| METRIC_TODAY_DAILY_USAGE | Enable aws_today_daily_usage metric      |
| METRIC_TODAY_DAILY_USAGE_NORM | Enable aws_today_daily_usage_norm metric      |


AWS IAM permission Settings:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "ce:*",
            "Resource": "*"
        }
    ]
}
```

Docker run:

Run on localhost
```
docker run -e METRIC_YESTERDAY_DAILY_COSTS=yes -e METRIC_TODAY_DAILY_COSTS=yes -p nexus.drsmile.co:8442/repository/prometheus/aws-cost-exporter:latest
```

