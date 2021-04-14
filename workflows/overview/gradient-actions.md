# Gradient Actions

Gradient Actions are composable building blocks for creating reproducible machine learning workflows. Actions use the `uses` and `with` syntax to specify how a job step executes.

### container

```yaml
uses: container@v1
with:
  image: bash:3
  args: ["echo", "hello", "world"]
```

In this basic example, the Gradient action called `container@v1` allows us to pick an arbitrary docker container \(in this case the lightweight `bash` container\) and pass arguments directly to it. 

### git-checkout

```yaml
uses: git-checkout@v1
with:
  url: https://github.com/user/public-repo
  ref: 46aa59d6ecc3720ffe2454a6d9d360e6ce75acce #optional git ref
```





