[Home](index) > [Developer](Developer) > [DevOps](DevOps) > **Helpful Kibana Queries**
***

The OpenShift Container Platform offers a Kibana interface for viewing the previous week of logs. Queries can be saved in Kibana so that they can be easily opened when needed.

Some helpful queries are:

#### API Calls:

This is useful to try to figure out why the database suddenly gets busy:
- Look at the metrics for the database primary and find the time period that the CPU was high
- Use the query below and set the Time Range to the period above
- Look at the API calls to try to see the problem. Maybe a single endpoint is repeatedly being accessed

```
kubernetes.namespace_labels.environment:prod AND kubernetes.container_name.raw:app AND message:"app/api/v1"
```

#### Application 500 Errors:

```
kubernetes.namespace_labels.environment:prod AND kubernetes.container_name.raw:app AND message:"\"statusCode\":500"
```

#### All Problems:

This is complicated a bit due to there being files with "error" in the name. Perhaps there's a simpler query that uses a regex?

```
kubernetes.namespace_labels.environment:prod AND /error|warn/ AND NOT message:"/app/assets/error" AND NOT message:"/app/js/error" AND NOT message:"/app/css/error" AND NOT message:"/app/error"
```

#### Database Problems:

```
kubernetes.namespace_labels.environment:prod AND kubernetes.container_name.raw:postgresql AND (message:"\"level\":\"error\"" OR message:"\"level\":\"warn\"")
```
