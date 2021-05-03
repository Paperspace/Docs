# Gradient Actions

Gradient Actions are composable building blocks for creating reproducible machine learning workflows. Actions use the `uses` and `with` syntax to specify how a job step executes.

## container

```yaml
uses: container@v1
with:
  image: bash:5
  args: ["echo", "hello", "world"]
```

In this basic example, the Gradient action called `container@v1` allows us to pick an arbitrary docker container \(in this case the lightweight `bash` container\) and pass arguments directly to it.

## script

```yaml
uses: script@v1
with:
  script: |-
    echo 'hello world'
    echo $RANDOM
  image: bash:5
```

If you want to run multiple commands, the `script@v1` action allows you to pass a `script` in a [literal-style HereDoc](https://lzone.de/cheat-sheet/YAML#yaml-heredoc-multiline-strings) denoted by `|-`. The pipe will preserve newlines and the dash will remove extra newlines after the block.

Note: The image you provide will need to have `bash` available in it's PATH.

## git-checkout

```yaml
inputs:
  repo:
    type: volume
uses: git-checkout@v1
with:
  url: https://github.com/user/my-public-repo
  ref: 46aa59d6ecc3720ffe2454a6d9d360e6ce75acce #optional git ref
```

In this example, the Gradient action `git-checkout@v1` clones the public GitHub URL `https://github.com/user/my-public-repo` at ref `46aa...` into a volume named `repo`. The cloned files are accessible at `inputs/<input-name>` \(in this case, `inputs/repo`\), and subsequent jobs that specify a volume input can also access the repository files at `inputs/<input-name>`.

Note: to clone a private repository, add your username as an action parameter, [set a Gradient secret](../../get-started/managing-projects/using-secrets.md#set-a-secret) with a [GitHub access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) value, and add your password as an environment variable named `GIT_PASSWORD` \(example below\).

```yaml
inputs:
  repo:
    type: volume
uses: git-checkout@v1
with:
  url: https://github.com/user/my-private-repo
  username: paperspace
env:
  GIT_PASSWORD: secret:<MY_SECRET_NAME>
```

## model-create

```yaml
inputs:
  model:
    type: dataset
    with:
      id: my-dataset
outputs:
  model-id:
    type: string
uses: create-model@v1
with:
  name: my-model-name
  type: Tensorflow #Tensorflow, ONNX, or Custom
```

In this example, the `create-model@v1` action takes a dataset input named `model` and outputs a string ID \(named `model-id`\) that references a [Gradient model](../../data/models/). With this reference, the created model can be tested, edited, or deployed in future jobs.

