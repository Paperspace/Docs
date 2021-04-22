---
description: How to query and view metrics in GUI and CLI
---

# View & Query Metrics

## Notebooks, Experiments & Deployment Metrics

{% tabs %}
{% tab title="Web GUI" %}
### Deployments

{% hint style="warning" %}
Deployment metrics are a Gradient Private Cluster feature. [Contact Sales](https://info.paperspace.com/contact-sales) for inquiries!
{% endhint %}

To view Deployment metrics, navigate to the Metrics tab of the individual deployment.

![](../../.gitbook/assets/image%20%2899%29%20%283%29%20%283%29%20%283%29%20%283%29%20%281%29.png)

### Notebooks

{% hint style="warning" %}
Notebook metrics are a Gradient Private Cluster feature. [Contact Sales](https://info.paperspace.com/contact-sales) for inquiries!
{% endhint %}

To view Notebook metrics, you will see a minimal version in the Notebook header and you can also open a more robust display with detailed information.  

![Detailed view](../../.gitbook/assets/image%20%28105%29%20%286%29%20%283%29%20%285%29.png)

![Collapsed view in Notebook header](../../.gitbook/assets/81246457-8a067200-8fcc-11ea-81c9-94fb4dea1eee.jpg)

### Workflows

Coming soon!
{% endtab %}

{% tab title="CLI" %}
To query the metrics for a given workload using the CLI.  Here's an example using Experiments \(the Deployments and Notebooks syntax are the same\).

```text
Usage: gradient experiments metrics [OPTIONS] COMMAND [ARGS]...

  Read experiment metrics

Options:
  --help  Show this message and exit.

Commands:
  get     Get experiment metrics
  stream  Watch live experiment metrics
  
```

### Get a single value for a given metric:

#### **Syntax**

```bash
gradient experiments metrics get --id <experiment id> 
```

#### **Parameters**

```bash
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

#### **Example command to get CPU usage in %:**

```bash
gradient experiments metrics get --id <experiment id> --metric cpuPercentage 
```

### Stream metrics:

#### Syntax

```bash
gradient experiments metrics stream --id <experiment id>
```

#### **Parameters**

```bash
Usage: gradient experiments metrics stream [OPTIONS]

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
{% endtab %}
{% endtabs %}





