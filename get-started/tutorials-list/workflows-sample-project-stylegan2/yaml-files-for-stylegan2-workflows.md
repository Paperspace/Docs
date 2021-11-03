# YAML files for StyleGAN2 workflows

These are the two YAML files used for the Workflows sample project based on StyleGAN2.

#### Download and extract data

```yaml
# StyleGAN2 Workflow 1 of 2: Download and extract data
#
# This is the YAML file used to run the Gradient download and extract data Workflow for the sample project based on
# StyleGAN2 at https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project .
#
# See that URL for details on how to run the project.
#
# We assume the reader is familiar with the basics of Workflows, and here wishes to use them for real projects.
#
# Steps performed by the Workflow
#
# 1. Download the cat image database as a .zip file
# 2. Clone StyleGAN2 repo for script that extracts images from the LMDB-format database
# 3. Unzip the .zip file and extract the images from the database into a Gradient managed dataset
#
# Dataset IDs
#
# The user needs to create their own Gradient managed datasets for job outputs, using the same names as here.
# See the project documentation for details on how to do this.
#
# Job name               Gradient managed dataset name
#
# getCatImageDatabase -> stylegan2-wsp-cat-img-db
# extractImages       -> stylegan2-wsp-extr-img
#
# Last updated: Sep 16th 2021

# Trigger Workflow to run on any update (commit) to the repository when linked to a Gradient project
# (uncomment to activate)
#
# An example of a change is to change the number of images extracted in the --max_images=1000 argument to the
# python dataset_tool.py create_lsun command in job 3 (extractImages) below

#on:
#  github:
#    branches:
#      only: main

# Our download and extract steps do not require a GPU, so we default to a C4 machine for all steps

defaults:
  resources:
    instance-type: C4 # C5 will run these steps faster if available, but costs more

jobs:

  # 1. Download the cat image database

  # The .zip file is about 45 gigabytes and the download takes about 30 minutes onto a Gradient machine
  # We compare its MD5 sum to the one available from the website to ensure we are using a consistent starting point
  # (they should be equal)

  getCatImageDatabase:
    outputs:
      catImageDatabase:
        type: dataset
        with:
          ref: stylegan2-wsp-cat-img-db
    uses: script@v1
    with:
      script: |-
        curl -o /outputs/catImageDatabase/cat.zip.md5 'http://dl.yf.io/lsun/objects/cat.zip.md5'
        curl -C - -o /outputs/catImageDatabase/cat.zip 'http://dl.yf.io/lsun/objects/cat.zip'
        cd /outputs/catImageDatabase
        echo "MD5 sum from downloaded file:"
        md5sum cat.zip
        echo "MD5 sum from website:"
        cat /outputs/catImageDatabase/cat.zip.md5
        ls "-aFlR" /outputs/catImageDatabase
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 2. Clone StyleGAN2 repo for script that extracts images from the LMDB-format database

  # The checkout results in an output volume
  # The repo is public so the "username:" field, and "env:" field containing a Git password are not needed

  cloneStyleGAN2Repo:
    outputs:
      repo:
        type: volume
    uses: git-checkout@v1
    with:
      url: https://github.com/NVlabs/stylegan2.git

  # 3. Unzip the .zip file and extract the images from the database into a Gradient managed dataset

  # The --max_images argument can be used to limit the number extracted to a subset if desired
  # Here we limit it to 1000 to give a reasonable model training time in the Modeling Workflow, but this can be increased
  # The extracted images then become the Gradient managed dataset that can be referred to in later steps
  # This avoids having to download the images again in those steps
  # The needed installations could also be done via a requirements.txt
  # /inputs is read-only so we do copy not move (mv) as move's delete step will fail
  # Note the repo gets put in /inputs/repo, not /inputs/repo/stylegan2
  # Note the Python and bash syntaxes that are placing those commands on one line within the "|-" script

  extractImages:
    needs:
      - getCatImageDatabase
      - cloneStyleGAN2Repo
    inputs:
      repo: cloneStyleGAN2Repo.outputs.repo
      catImageDatabase: getCatImageDatabase.outputs.catImageDatabase
    outputs:
      extractedImages:
        type: dataset
        with:
          ref: stylegan2-wsp-extr-img
    uses: script@v1
    with:
      script: |-
        cd /inputs/catImageDatabase
        mkdir -p /cat_workspace/catImagesUnzipped
        unzip cat.zip -d /cat_workspace/catImagesUnzipped
        pip install --upgrade pip
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        pip install lmdb==1.2.1
        pip install python-lmdb==1.0.0b1
        apt-get update
        apt-get install ffmpeg libsm6 libxext6 -y
        pip install opencv-python==4.5.1.48
        cp -R /inputs/repo /stylegan2
        cd /stylegan2
        python dataset_tool.py create_lsun \
          /outputs/extractedImages/cat_images_tfrecords \
          /cat_workspace/catImagesUnzipped/cat \
          --resolution=256 \
          --max_images=1000
        rm -r /cat_workspace/catImagesUnzipped
        cd /outputs/extractedImages/cat_images_tfrecords
        mkdir cat
        mv *.tfrecords cat
        ls "-aFlR" /outputs/extractedImages
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # Appendix: Extra details
  #
  # Some other notes on what some steps above are doing and why
  #
  #  - The StyleGAN2 repo's download script is for the Flickr Faces Dataset, and
  #    LSUN's download script is for their scene categories dataset, but not object categories
  #  - The cat data under object categories has no download script, hence curl http://dl.yf.io/lsun/objects/cat.zip
  #  - getCatImageDatabase uses TensorFlow image because alpine:latest doesn't have bash, and bash:5 doesn't have curl
  #  - This works, and other images could also be used
  #  - /cat_workspace is acting like a temporary volume (copy files to it then rm), which could be done more formally
  #  - pip install --upgrade pip helps the opencv install go considerably faster
  #  - lmdb, python-lmdb, and opencv are required for dataset_tool.py create_lsun
  #  - The apt-get commands are needed for OpenCV on this container
  #  - The subdirectory /outputs/extractedImages/cat is needed so dataset_tool.py, etc., can locate the images
```

#### Train and evaluate model

```yaml
# StyleGAN2 Workflow 2 of 2: Train and evaluate model
#
# This is the YAML file used to run the Gradient modeling Workflow for the sample project based on StyleGAN2 at
# https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project .
#
# See that URL for details on how to run the project.
#
# We assume the reader is familiar with the basics of Workflows, and here wishes to use them for real projects.
#
# Steps performed by the Workflow
#
# 1. Clone StyleGAN repo into managed storage provider dataset
# 2. Get pretrained cat model
# 3. Run evaluation on pretrained cat model
# 4. Show generating images using pretrained cat model
# 5. Train our model on image subsample
# 6. Run evaluation on our trained model
# 7. Show generating images with our trained model
#
# Dataset IDs
#
# The user needs to create their own Gradient managed datasets for job outputs, using the same names as here.
# See the project documentation for details on how to do this.
#
# Job name                         Gradient managed dataset name
#
# getPretrainedModel            -> stylegan2-wsp-pretrained-network
# evaluatePretrainedModel       -> stylegan2-wsp-evaluation-pretrained
# generateImagesPretrainedModel -> stylegan2-wsp-generated-cats-pretrained
# trainOurModel                 -> stylegan2-wsp-our-trained-network
# evaluateOurModel              -> stylegan2-wsp-evaluation-ours
# generateImagesOurModel        -> stylegan2-wsp-generated-cats-ours
#
# The names for the Gradient managed datasets should correspond to the names output from running the first workflow of
# the pair in this project (stylegan2-download-and-extract-data.yaml).
#
# We create different datasets for the output from each job because jobs can run in parallel and if their outputs were
# put into the same dataset it would create clashing versions.
#
# Last updated: Sep 16th 2021

# Trigger Workflow to run on any update (commit) to the repository when linked to a Gradient project
# (uncomment to activate)
#
# An example of a change is to change the random seeds for image generation in the --seeds=6600-6605 argument to the
# python run_generator.py generate-images command in job 4 (generateImagesPretrainedModel) below

#on:
#  github:
#    branches:
#      only: main

jobs:

  # 1. Clone StyleGAN repo into managed storage provider dataset

  cloneStyleGAN2Repo:
    resources:
      instance-type: C4
    outputs:
      repo:
        type: volume
    uses: git-checkout@v1
    with:
      url: https://github.com/NVlabs/stylegan2.git

  # 2. Get pretrained cat model

  # The model .pkl is large so is not in the main StyleGAN2 repo
  # We copy the .pkl in this step, then refer to the copy via getPretrainedModel.outputs.pretrainedNetwork
  # below to avoid copying it again in the next steps

  getPretrainedModel:
    resources:
      instance-type: C4
    outputs:
      pretrainedNetwork:
        type: dataset
        with:
          ref: stylegan2-wsp-pretrained-network
    uses: container@v1
    with:
      args:
        - wget
        - https://nvlabs-fi-cdn.nvidia.com/stylegan2/networks/stylegan2-cat-config-f.pkl
        - -P
        - /outputs/pretrainedNetwork
      image: alpine:latest

  # 3. Run evaluation on pretrained cat model

  # The input extracted images dataset reference refers to the latest version from Workflow 1
  # A particular version of the input extracted images can also be specified, via <dataset ID>:<dataset version>
  # (Also available are no version (latest), v1 (etc.), :latest, or :<dataset-tag>)

  # Comment the first "ref:" line and uncomment the second one under "inputs:" below if you ran Workflow 1 yourself and
  # want to use its output rather than gradient/stylegan2-workflows-sample-project-extr-img, which is the public dataset

  evaluatePretrainedModel:
    resources:
      instance-type: P4000 # P6000 or V100 will run this step faster if available, but cost more
    needs:
      - cloneStyleGAN2Repo
      - getPretrainedModel
    inputs:
      repo: cloneStyleGAN2Repo.outputs.repo
      extractedImagesForTraining:
        type: dataset
        with:
          ref: gradient/stylegan2-workflows-sample-project-extr-img
          #ref: stylegan2-wsp-extr-img
      pretrainedNetwork: getPretrainedModel.outputs.pretrainedNetwork
    outputs:
      evaluationPretrained:
        type: dataset
        with:
          ref: stylegan2-wsp-evaluation-pretrained
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
        cd /stylegan2
        python run_metrics.py \
          --data-dir=/stylegan2/cat_images_tfrecords \
          --network=/inputs/pretrainedNetwork/stylegan2-cat-config-f.pkl \
          --metrics=fid50k,ppl2_wend \
          --dataset=cat \
          --result-dir=/outputs/evaluationPretrained
        ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 4. Show generating images using pretrained cat model

  generateImagesPretrainedModel:
    resources:
      instance-type: P4000
    needs:
      - cloneStyleGAN2Repo
      - getPretrainedModel
    inputs:
      repo: cloneStyleGAN2Repo.outputs.repo
      pretrainedNetwork: getPretrainedModel.outputs.pretrainedNetwork
    outputs:
      generatedCatsPretrained:
        type: dataset
        with:
          ref: stylegan2-wsp-generated-cats-pretrained
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cd /stylegan2
        python run_generator.py generate-images \
          --network=/inputs/pretrainedNetwork/stylegan2-cat-config-f.pkl \
          --seeds=6600-6605 \
          --truncation-psi=0.5 \
          --result-dir=/outputs/generatedCatsPretrained
        ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 5. Train our model on image subsample

  # This could be extended to a larger image set by passing it in instead

  # Comment the first "ref:" line and uncomment the second one under "inputs:" below if you ran Workflow 1 yourself and
  # want to use its output rather than gradient/stylegan2-workflows-sample-project-extr-img, which is the public dataset

  trainOurModel:
    resources:
      instance-type: P4000 # Or P6000, V100
    needs:
      - cloneStyleGAN2Repo
    inputs:
      extractedImagesForTraining:
        type: dataset
        with:
          ref: gradient/stylegan2-workflows-sample-project-extr-img
          #ref: stylegan2-wsp-extr-img
      repo: cloneStyleGAN2Repo.outputs.repo
    outputs:
      ourTrainedNetwork:
        type: dataset
        with:
          ref: stylegan2-wsp-our-trained-network
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
        cd /stylegan2
        python run_training.py \
          --data-dir=/stylegan2/cat_images_tfrecords \
          --config=config-f \
          --dataset=cat \
          --total-kimg=10 \
          --result-dir=/outputs/ourTrainedNetwork
        ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 6. Run evaluation on our trained model

  # Note here we are evaluating on the same images as used for training
  # Since our model was only trained on a small subset it doesn't matter here

  # Comment the first "ref:" line and uncomment the second one under "inputs:" below if you ran Workflow 1 yourself and
  # want to use its output rather than gradient/stylegan2-workflows-sample-project-extr-img, which is the public dataset

  evaluateOurModel:
    resources:
      instance-type: P4000 # Or P6000, V100
    needs:
      - cloneStyleGAN2Repo
      - trainOurModel
    inputs:
      repo: cloneStyleGAN2Repo.outputs.repo
      extractedImagesForTraining:
        type: dataset
        with:
          ref: gradient/stylegan2-workflows-sample-project-extr-img
          #ref: stylegan2-wsp-extr-img
      ourTrainedNetwork: trainOurModel.outputs.ourTrainedNetwork
    outputs:
      evaluationOurs:
        type: dataset
        with:
          ref: stylegan2-wsp-evaluation-ours
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
        cp    /inputs/ourTrainedNetwork/00000-stylegan2-cat-1gpu-config-f/network-final.pkl /stylegan2
        cd /stylegan2
        python run_metrics.py \
          --data-dir=/stylegan2/cat_images_tfrecords \
          --network=/stylegan2/network-final.pkl \
          --metrics=fid50k,ppl2_wend \
          --dataset=cat \
          --result-dir=/outputs/evaluationOurs
        ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 7. Show generating images with our trained model

  generateImagesOurModel:
    resources:
      instance-type: P4000
    needs:
      - cloneStyleGAN2Repo
      - trainOurModel
    inputs:
      repo: cloneStyleGAN2Repo.outputs.repo
      ourTrainedNetwork: trainOurModel.outputs.ourTrainedNetwork
    outputs:
      generatedCatsOurs:
        type: dataset
        with:
          ref: stylegan2-wsp-generated-cats-ours
    uses: script@v1
    with:
      script: |-
        pip install scipy==1.3.3
        pip install requests==2.22.0
        pip install Pillow==6.2.1
        cp -R /inputs/repo /stylegan2
        cp    /inputs/ourTrainedNetwork/00000-stylegan2-cat-1gpu-config-f/network-final.pkl /stylegan2
        cd /stylegan2
        python run_generator.py generate-images \
          --network=/stylegan2/network-final.pkl \
          --seeds=6600-6605 \
          --truncation-psi=0.5 \
          --result-dir=/outputs/generatedCatsOurs
        ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3
```
