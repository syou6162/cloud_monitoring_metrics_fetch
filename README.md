## cloud_monitoring_metrics_fetch
`cloud_monitoring_metrics_fetch` is a command line tool to extract metrics from cloud monitoirng metrics.

## Install

```
go install github.com/syou6162/cloud_monitoring_metrics_fetch@latest
```

## Usage
You can fetch metrics from cloud monitoring by JSON format.

```
cloud_monitoring_metrics_fetch \
  --project my-project \
  --metricType compute.googleapis.com/instance/cpu/utilization \
  --resourceType gce_instance \
  --start (gdate --date '10 days ago' '+%s') \
  --end (gdate '+%s') | \
  jq -c '.[]' > out.json
```

You can load metrics data to BigQuery like following command.

```
bq --project_id=my-project load --replace --source_format=NEWLINE_DELIMITED_JSON --encoding=UTF-8 my_dataset.my_table out.json schema.json
```
