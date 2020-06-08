---
description: How to query and view metrics in GUI and CLI
---

# Query Metrics

## Experiments metrics

{% tabs %}
{% tab title="Web GUI" %}
You can view metrics for experiments by clicking on the individual jobs that represent worker nodes and then entering "Metrics" Tab:

![](../.gitbook/assets/screenshot-metrics.jpg)
{% endtab %}

{% tab title="CLI" %}
To query the metrics for given experiment using the CLI:

```text
Usage: gradient experiments metrics [OPTIONS] COMMAND [ARGS]...

  Read experiment metrics

Options:
  --help  Show this message and exit.

Commands:
  get     Get experiment metrics
  stream  Watch live experiment metrics
  
```

### Get single value for given metric:

```text
Usage: gradient experiments metrics get [OPTIONS]

  Get experiment metrics. Shows CPU and RAM usage by default

Options:
  --id TEXT                       ID of the experiment  [required]
  --metric [cpuPercentage|memoryUsage|gpuMemoryFree|gpuMemoryUsed|gpuPowerDraw|gpuTemp|gpuUtilization|gpuMemoryUtilization]
                                  One or more metrics that you want to read.
                                  Defaults to cpuPercentage and memoryUsage
  --interval TEXT                 Interval
  --start [%Y-%m-%d|%Y-%m-%dT%H:%M:%S|%Y-%m-%d %H:%M:%S]
                                  Timestamp of first time series metric to
                                  collect
  --end [%Y-%m-%d|%Y-%m-%dT%H:%M:%S|%Y-%m-%d %H:%M:%S]
                                  Timestamp of last time series metric to
                                  collect
  --apiKey TEXT                   API key to use this time only
  --optionsFile PATH              Path to YAML file with predefined options
  --createOptionsFile PATH        Generate template options file
  --help                          Show this message and exit.
  
```

example command to get CPU usage in %:

```text
gradient experiments metrics get --id <experiment id> --metric cpuPercentage 
```

### Stream metrics:

```text
gradient experiments metrics stream --id <experiment id>
```

Usage: gradient experiments metrics stream \[OPTIONS\]

Watch live experiment metrics. Shows CPU and RAM usage by default

Options:

* id: ID of the experiment \[required\] 
* metric: 
  * cpuPercentage
  * memoryUsage
  * gpuMemoryFree
  * gpuMemoryUsed
  * gpuPowerDraw
  * gpuTemp
  * gpuUtilization
  * gpuMemoryUtilization 
* interval TEXT Interval
{% endtab %}
{% endtabs %}

