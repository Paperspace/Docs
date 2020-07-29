---
description: How to push metrics into Gradient Metrics system
---

# Push Metrics

In order to push metrics from your Experiment or Deployment code, you must import gradient-utils from gradient package:

### Installing Gradient Utils

```text
pip install gradient-utils
```

### Instrumenting

Four types of metrics are offered: Counter, Gauge, Summary, and Histogram. 

#### Counter

Counters go up, and reset when the process restarts.

```text
from gradient_utils.metrics import Counter
c = Counter('my_failures', 'Description of counter')
c.inc()     # Increment by 1
c.inc(1.6)  # Increment by given value
```

If there is a suffix of `_total` on the metric name, it will be removed. When exposing the time series for counter, a `_total` suffix will be added. This is for compatibility between OpenMetrics and the Prometheus text format, as OpenMetrics requires the `_total` suffix.

There are utilities to count exceptions raised:

```text
@c.count_exceptions()
def f():
  pass

with c.count_exceptions():
  pass

# Count only one type of exception
with c.count_exceptions(ValueError):
  pass
```

#### Gauge

Gauges can go up and down.

```text
from gradient_utils.metrics import Gauge
g = Gauge('my_inprogress_requests', 'Description of gauge')
g.inc()      # Increment by 1
g.dec(10)    # Decrement by given value
g.set(4.2)   # Set to a given value
```

There are utilities for common use cases:

```text
g.set_to_current_time()   # Set to current unixtime

# Increment when entered, decrement when exited.
@g.track_inprogress()
def f():
  pass

with g.track_inprogress():
  pass
```

A Gauge can also take its value from a callback:

```text
d = Gauge('data_objects', 'Number of objects')
my_dict = {}
d.set_function(lambda: len(my_dict))
```

#### Summary

Summaries track the size and number of events.

```text
from gradient_utils.metrics import Summary
s = Summary('request_latency_seconds', 'Description of summary')
s.observe(4.7)    # Observe 4.7 (seconds in this case)
```

There are utilities for timing code:

```text
@s.time()
def f():
  pass

with s.time():
  pass
```

The Python client doesn't store or expose quantile information at this time.

#### Histogram

Histograms track the size and number of events in buckets. This allows for aggregatable calculation of quantiles.

```text
from gradient_utils.metrics import Histogram
h = Histogram('request_latency_seconds', 'Description of histogram')
h.observe(4.7)    # Observe 4.7 (seconds in this case)
```

The default buckets are intended to cover a typical web/rpc request from milliseconds to seconds. They can be overridden by passing `buckets` keyword argument to `Histogram`.

There are utilities for timing code:

```text
@h.time()
def f():
  pass

with h.time():
  pass
```

#### Labels

All metrics can have labels, allowing grouping of related time series.

Taking a counter as an example:

```text
from gradient_utils.metrics import Counter
c = Counter('my_requests_total', 'HTTP Failures', ['method', 'endpoint'])
c.labels('get', '/').inc()
c.labels('post', '/submit').inc()
```

Labels can also be passed as keyword-arguments:

```text
from gradient_utils.metrics import Counter
c = Counter('my_requests_total', 'HTTP Failures', ['method', 'endpoint'])
c.labels(method='get', endpoint='/').inc()
c.labels(method='post', endpoint='/submit').inc()
```

### Example Code

```text
from gradient_utils.metrics import MetricsLogger

logger = MetricsLogger(grouping_key={'ProjectA': 'SomeLabel'})

logger.add_gauge("Gauge")
logger.add_counter("Counter")


while datetime.now() <= endAt:
    randNum = randint(1, 100)
    logger["Gauge"] = 5
    logger["Gauge"].set(randNum)
    logger["Counter"].inc()
    logger.push_metrics()
```

You have to remember to import MetricsLogger:

```text
from gradient_utils.metrics import MetricsLogger
```

## Notes:

Gradient uses [Prometheus](https://prometheus.io/) behind the scenes. See the Prometheus documentation on [metric types](http://prometheus.io/docs/concepts/metric_types/) and [instrumentation best practices](https://prometheus.io/docs/practices/instrumentation/#counter-vs-gauge-summary-vs-histogram) the best practices on [naming](http://prometheus.io/docs/practices/naming/) and [labels](http://prometheus.io/docs/practices/instrumentation/#use-labels) on how to use them.  

