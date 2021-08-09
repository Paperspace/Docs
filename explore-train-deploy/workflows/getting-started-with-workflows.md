# Creating and Running Workflows

The following sections cover creating and running workflows, and authoring new workflow yaml specs.  If you have never run a workflow before we recommend you step through the workflows demo in the [quick-start guide](https://docs.paperspace.com/gradient/get-started/quick-start#create-a-project) then return here for more details.

## Creating Gradient Workflows

{% hint style="info" %}
View the full CLI/SDK Docs for **Workflows** here [https://paperspace.github.io/gradient-cli/gradient.cli.html\#gradient-workflows](https://paperspace.github.io/gradient-cli/gradient.cli.html#gradient-workflows)
{% endhint %}

1. Make sure you have the latest version of the [Gradient CLI](../../get-started/quick-start/install-the-cli.md)
2. Create a [Gradient Project](../../get-started/managing-projects/) and [grab your project ID](../../get-started/managing-projects/#get-your-projects-id)
3. Create your first workflow using the Gradient CLI

```bash
gradient workflows create --name <my-workflow-name> --projectId <project-id>
```
The command will return an ID for the workflow, for example, `7634c165-5034-4f49-95fa-005fc0e7970b`.

## Running a Workflow

First create a valid workflow spec yaml file.  Here is an example **workflow.yaml** spec you can use:
```yaml
jobs:
  CloneRepo:
    resources:
      instance-type: C5
    outputs:
      repo:
        type: volume
    uses: git-checkout@v1
    with:
      url: https://github.com/NVlabs/stylegan2.git
  StyleGan2:
    resources:
      instance-type: P4000
    needs:
      - CloneRepo
    inputs:
      repo: CloneRepo.outputs.repo
    outputs:
      generatedFaces:
        type: dataset
        with:
          ref: dsrlylvgje7q6zl
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cd /stylegan2
        python run_generator.py generate-images \
          --network=gdrive:networks/stylegan2-ffhq-config-f.pkl \
          --seeds=6600-6605 \
          --truncation-psi=0.5 \
          --result-dir=/outputs/generatedFaces
      image: tensorflow/tensorflow:1.14.0-gpu-py3
```

You will also need a
**`workflow-id`** from the previously created workflow. (You can also get one by running `gradient workflows list` in the CLI.)
```bash
gradient workflows run  \
    --id <worklow-id> \ 
    --path ./workflow.yaml
```
A workflow run can be performed multiple times, each with the same or a different workflow yaml spec.  The workflow spec is recorded as part of the workflow run so that you can distinguish the different runs.

The next sections cover the syntax and concepts behind authoring new workflow yaml specs for MLops applications.
