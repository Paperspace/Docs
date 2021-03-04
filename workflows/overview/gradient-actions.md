# Gradient Actions

Gradient Actions are composable building blocks for creating reproducible machine learning workflows. Actions use the `uses` and `with` syntax to specify how a job step executes.

```yaml
uses: container@v1
with:
  image: bash:3
  args: ["echo", "hello", "world"]
```

In this basic example, the Gradient action called `container@v1` allows us to pick an arbitrary docker container \(in this case the lightweight `bash` container\) and pass arguments directly to it. 



