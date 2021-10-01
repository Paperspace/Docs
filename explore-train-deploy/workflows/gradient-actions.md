# Gradient Actions

Gradient Actions are composable building blocks for creating reproducible machine learning Workflows. Actions use the `uses` and `with` syntax to specify how a job step executes.

## container

```yaml
uses: container@v1
with:
  image: bash:5
  args: ["echo", "hello", "world"]
```

The Gradient Action called `container@v1` allows you to use an arbitrary Docker container image \(in this case the lightweight `bash` container image\) and pass arguments directly to it.

## script

```yaml
uses: script@v1
with:
  script: |-
    echo 'hello world'
    echo $RANDOM
  image: bash:5
```

If you want to run multiple commands, the `script@v1` action allows you to pass a `script` in a [literal-style HereDoc](https://lzone.de/cheat-sheet/YAML#yaml-heredoc-multiline-strings) denoted by `|-`. The pipe character will preserve newlines and the dash will remove extra newlines after the block.

_Note:_ The image you provide will need to have `bash` available in its PATH.

## git-checkout

```yaml
outputs:
  repo:
    type: volume
uses: git-checkout@v1
with:
  url: https://github.com/user/my-public-repo
  ref: 46aa59d6ecc3720ffe2454a6d9d360e6ce75acce # Optional git ref
  path: /outputs/repo # Optional, defaults to exactly one output volume or dataset
```

In this example, the Gradient Action `git-checkout@v1` clones the public GitHub URL `https://github.com/user/my-public-repo` at ref `46aa...` into a volume named `repo`. The cloned files are accessible at `/outputs/<output-name>` \(in this case, `/outputs/repo`\), and subsequent jobs that specify the checkout job's volume as an input can also access the repository files as read-only at `/inputs/<input-name>`.

```yaml
inputs:
  repo: checkout-job.outputs.repo
uses: container@v1
with:
  image: busybox
  args: ['ls', '/inputs/repo']
```

_Note:_ To clone a private repository, add your username as a parameter, [set a Gradient secret](../../get-started/managing-projects/using-secrets.md#set-a-secret) with a [GitHub access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) value, and add a password parameter:

```yaml
outputs:
  repo:
    type: volume
uses: git-checkout@v1
with:
  url: https://github.com/user/my-private-repo
  username: paperspace
  password: secret:MY_SECRET_NAME
```

You can also use `path` to pick an output target:

```yaml
outputs:
  repo:
    type: volume
  ds:
    type: dataset
    with:
      ref: my-dataset
uses: git-checkout@v1
with:
  url: https://github.com/user/my-public-repo
  ref: 46aa59d6ecc3720ffe2454a6d9d360e6ce75acce # Optional git ref
  path: /outputs/repo/subfolder
```

## s3-download

```yaml
outputs:
  s3:
    type: volume
uses: s3-download@v1
with:
  url: s3://bucket/path/
  access-key: MYACCESSKEY
  secret-access-key: secret:MY_SECRET_NAME
```

The `s3-download@v1` Gradient Action copies the contents of an Amazon S3 bucket into an output \(in this example, the volume is named `s3`\). Subsequent jobs that specify an input that reference the `s3-download` job's volume output can access the downloaded files within that job at `/inputs/<input-name>`.

_Note:_ `access-key` and `secret-access-key` are required parameters, and the latter must be a [Gradient secret](../../get-started/managing-projects/using-secrets.md#set-a-secret). Optional parameters include `region` \(for AWS buckets\), `endpoint` \(for non-AWS buckets\), and `path` \(to disambiguate target outputs or to download to a subfolder\).

## model-create

```yaml
inputs:
  model:
    type: dataset
    with:
      ref: dsr8k5qzn401lb5:klfoyy9 # Example dataset ref
outputs:
  model-id:
    type: string
uses: create-model@v1
with:
  name: my-model-name
  type: Tensorflow # Tensorflow, ONNX, or Custom
```

In this example, the `create-model@v1` action takes a dataset input named `model` and outputs a string ID \(named `model-id`\) that references a [Gradient model](../../data/models/). With this reference, the created model can be tested, edited, or deployed in future jobs.

