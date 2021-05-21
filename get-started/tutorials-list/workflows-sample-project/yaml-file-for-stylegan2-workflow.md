# YAML file for StyleGAN2 workflows

These are the YAML files used for the Workflows sample project based on StyleGAN2.

### Download and extract data

```yaml
# StyleGAN2 Workflow 1 of 2: Download and extract data
#
# This is the YAML file used to run the Gradient download and extract data Workflow for the sample project based on
# StyleGAN2 at https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project .
#
# See that URL for details on how to run the project.
#
# We assume the reader is familiar with the basics of workflows, and here wishes to use them for real projects.
#
# Workflow steps
#
# 1. Download the cat image database as a .zip file
# 2. Clone StyleGAN2 repo for script that extracts images from the LMDB-format database
# 3. Unzip the .zip file and extract the images from the database into a Gradient managed dataset
#
# Dataset IDs
#
# The user needs to create their own Gradient managed datasets for job outputs to replace the IDs this file contains:
#
# getCatImageDatabase -> "dstlbm17s9ib1ld"
# extractImages       -> "dstfq4pfrtz4fav"
#
# Last updated: May 20th 2021

# Our download and extract steps do not require a GPU, so we default to a C5 machine for all steps

defaults:
  resources:
    instance-type: C5

jobs:

  # 1. Download the cat image database

  # The .zip file is about 45 gigabytes and the download takes about 30 minutes onto a Gradient machine
  # We compare its MD5 sum to the one available from the website to ensure we are using a consistent starting point
  # (they should be equal)
  # The temporary workaround using gzip/split/cat/gunzip is visible here and in step 3

  getCatImageDatabase:
    outputs:
      catImageDatabase:
        type: dataset
        with:
          id: "dstlbm17s9ib1ld"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          curl -o /outputs/catImageDatabase/cat.zip.md5 'http://dl.yf.io/lsun/objects/cat.zip.md5'
          curl -C - -o /outputs/catImageDatabase/cat.zip 'http://dl.yf.io/lsun/objects/cat.zip'
          cd /outputs/catImageDatabase
          split -a 3 -b 100m cat.zip cat_files_
          echo "MD5 sum from downloaded file:"
          md5sum cat.zip
          echo "MD5 sum from website:"
          cat /outputs/catImageDatabase/cat.zip.md5
          rm cat.zip
          ls "-aFlR" /outputs/catImageDatabase
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 2. Clone StyleGAN2 repo for script that extracts images from the LMDB-format database

  # Checkout results in an output volume, so we don't need the "outputs:" field
  # The repo is public so the "username:" field, and "env:" field containing a Git password are not needed

  cloneStyleGAN2Repo:
    inputs:
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
  # /inputs is read-only so we do copy not move as move's delete step will fail
  # Note the repo gets put in /inputs/repo, not /inputs/repo/stylegan2
  # Note the Python and bash syntaxes that are placing those commands on one line within the "|-" script

  extractImages:
    needs:
      - getCatImageDatabase
      - cloneStyleGAN2Repo
    inputs:
      repo:
        type: volume
      catImageDatabase: getCatImageDatabase.outputs.catImageDatabase
    outputs:
      extractedImages:
        type: dataset
        with:
          id: "dstfq4pfrtz4fav"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          cd /inputs/catImageDatabase
          mkdir -p /cat_workspace/catImagesReconstructed
          mkdir /cat_workspace/catImagesUnzipped
          cat cat_files_* > /cat_workspace/catImagesReconstructed/cat_reconstructed.zip
          md5sum /cat_workspace/catImagesReconstructed/cat_reconstructed.zip
          unzip /cat_workspace/catImagesReconstructed/cat_reconstructed.zip -d /cat_workspace/catImagesUnzipped
          rm /cat_workspace/catImagesReconstructed/cat_reconstructed.zip
          pip install --upgrade pip
          pip install scipy==1.3.3
          pip install requests==2.22.0
          pip install Pillow==6.2.1
          pip install lmdb==1.2.1
          pip install python-lmdb==1.0.0b1
          apt-get update
          apt-get install ffmpeg libsm6 libxext6  -y
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
          cd cat
          for res in 2 3 4 5 6 7 8; do \
            gzip cat_images_tfrecords-r0$res.tfrecords; \
            split -a 3 -b 100m cat_images_tfrecords-r0$res.tfrecords.gz cat_images_tfrecords-r0${res}_; \
          done
          rm cat_images_tfrecords-r0?.tfrecords.gz
          ls "-aFlR" /outputs/extractedImages
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # Appendix: Extra details
  #
  # Some other notes on what some steps above are doing and why
  #
  #  - The cat data has no download script, hence curl http://dl.yf.io/lsun/objects/cat.zip
  #  - The StyleGAN2 repo's download script is for the Flickr Faces Dataset, and
  #    LSUN's download script is for their scene categories dataset, not object categories
  #  - getCatImageDatabase uses TensorFlow image because alpine:latest doesn't have bash, and bash:5 doesn't have curl
  #  - /cat_workspace is acting like a temporary volume (copy files to it then rm), which could be done more formally
  #  - The "|-" bash script form could also use the new script@v1 Gradient action
  #  - pip install --upgrade pip helps the opencv install go considerably faster
  #  - lmdb, python-lmdb, and opencv are required for dataset_tool.py create_lsun
  #  - The apt-get commands are needed for OpenCV on this container
  #  - The subdirectory /outputs/extractedImages/cat is needed so dataset_tool.py can locate the images

```

### Train and evaluate model

```yaml
# StyleGAN2 Workflow 2 of 2: Train and evaluate model
#
# This is the YAML file used to run the Gradient modeling Workflow for the sample project based on StyleGAN2 at
# https://docs.paperspace.com/gradient/get-started/tutorials-list/workflows-sample-project .
#
# See that URL for details on how to run the project.
#
# We assume the reader is familiar with the basics of workflows, and here wishes to use them for real projects.
#
# Workflow steps
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
# The user needs to create their own Gradient managed datasets for job outputs to replace the IDs this file contains:
#
# getPretrainedModel            -> "dsr4si1mzvjyls8"
# evaluatePretrainedModel       -> "dsr7sry8b6mkzmi"
# generateImagesPretrainedModel -> "dsrtxabxfqmjbrw"
# trainOurModel                 -> "dsrso5rn4vtjlf4"
# evaluateOurModel              -> "dstp3of0i4tr38s"
# generateImagesOurModel        -> "dstba8lqk9g2x7v"
#
# The ID for the Gradient managed dataset should correspond to the ID and version output from running the first workflow
# of the pair in this project (stylegan2-download-and-extract-data.yaml)
#
# We create different datasets for the output from each job because jobs can run in parallel and if their outputs were
# put into the same dataset it would create clashing versions.
#
# Last updated: May 20th 2021

jobs:

  # 1. Clone StyleGAN repo into managed storage provider dataset

  cloneStyleGAN2Repo:
    resources:
      instance-type: C5
    inputs:
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
      instance-type: C5
    outputs:
      pretrainedNetwork:
        type: dataset
        with:
          id: "dsr4si1mzvjyls8"
    uses: container@v1
    with:
      args:
        - wget
        - https://nvlabs-fi-cdn.nvidia.com/stylegan2/networks/stylegan2-cat-config-f.pkl
        - -P
        - /outputs/pretrainedNetwork
      image: alpine:latest

  # 3. Run evaluation on pretrained cat model

  # The temporary workaround using gzip/split/cat/gunzip is visible here and in steps 5-7
  # dsts5p5o8fe86j3:6qstm0t refers to the specific dataset version that we want here
  # (Also available are no version (latest), v1 (etc.), :latest, or :<dataset-tag>)

  evaluatePretrainedModel:
    resources:
      instance-type: V100
    needs:
      - cloneStyleGAN2Repo
      - getPretrainedModel
    inputs:
      repo:
        type: volume
      extractedImagesForTraining:
        type: dataset
        with:
          id: "dstfq4pfrtz4fav:17dcxcj"
      pretrainedNetwork: getPretrainedModel.outputs.pretrainedNetwork
    outputs:
      evaluationPretrained:
        type: dataset
        with:
          id: "dsr7sry8b6mkzmi"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          pip install scipy==1.3.3
          pip install requests==2.22.0
          pip install Pillow==6.2.1
          cp -R /inputs/repo /stylegan2
          cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
          cd /stylegan2/cat_images_tfrecords/cat
          for res in 2 3 4 5 6 7 8; do \
            cat cat_images_tfrecords-r0${res}_* > cat_images_tfrecords-r0$res.tfrecords.gz; \
            gunzip cat_images_tfrecords-r0$res.tfrecords.gz; \
          done
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
      repo:
        type: volume
      pretrainedNetwork: getPretrainedModel.outputs.pretrainedNetwork
    outputs:
      generatedCatsPretrained:
        type: dataset
        with:
          id: "dsrtxabxfqmjbrw"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
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

  # This could be extended to a larger image set by passing it in instead of dsts5p5o8fe86j3:6qstm0t

  trainOurModel:
    resources:
      instance-type: V100
    needs:
      - cloneStyleGAN2Repo
    inputs:
      extractedImagesForTraining:
        type: dataset
        with:
          id: "dstfq4pfrtz4fav:17dcxcj"
      repo:
        type: volume
    outputs:
      ourTrainedNetwork:
        type: dataset
        with:
          id: "dsrso5rn4vtjlf4"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          pip install scipy==1.3.3
          pip install requests==2.22.0
          pip install Pillow==6.2.1
          cp -R /inputs/repo /stylegan2
          cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
          cd /stylegan2/cat_images_tfrecords/cat
          for res in 2 3 4 5 6 7 8; do \
            cat cat_images_tfrecords-r0${res}_* > cat_images_tfrecords-r0$res.tfrecords.gz; \
            gunzip cat_images_tfrecords-r0$res.tfrecords.gz; \
          done
          cd /stylegan2
          python run_training.py \
            --data-dir=/stylegan2/cat_images_tfrecords \
            --config=config-f \
            --dataset=cat \
            --total-kimg=10 \
            --result-dir=/outputs/ourTrainedNetwork
          cd /outputs/ourTrainedNetwork/00000-stylegan2-cat-1gpu-config-f
          gzip network-final.pkl
          split -a 3 -b 100m network-final.pkl.gz network-final_
          rm network-final.pkl.gz network-snapshot-*
          ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

  # 6. Run evaluation on our trained model

  # Note here we are evaluating on the same images as used for training
  # Since our model was only trained on a small subset it doesn't matter here

  evaluateOurModel:
    resources:
      instance-type: V100
    needs:
      - cloneStyleGAN2Repo
      - trainOurModel
    inputs:
      repo:
        type: volume
      extractedImagesForTraining:
        type: dataset
        with:
          id: "dstfq4pfrtz4fav:17dcxcj"
      ourTrainedNetwork: trainOurModel.outputs.ourTrainedNetwork
    outputs:
      evaluationOurs:
        type: dataset
        with:
          id: "dstp3of0i4tr38s"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          pip install scipy==1.3.3
          pip install requests==2.22.0
          pip install Pillow==6.2.1
          cp -R /inputs/repo /stylegan2
          cp -R /inputs/extractedImagesForTraining/cat_images_tfrecords /stylegan2
          cd /stylegan2/cat_images_tfrecords/cat
          for res in 2 3 4 5 6 7 8; do \
            cat cat_images_tfrecords-r0${res}_* > cat_images_tfrecords-r0$res.tfrecords.gz; \
            gunzip cat_images_tfrecords-r0$res.tfrecords.gz; \
          done
          mkdir /ourTrainedNetwork
          cd /ourTrainedNetwork
          cat /inputs/ourTrainedNetwork/00000-stylegan2-cat-1gpu-config-f/network-final_* > network-final.pkl.gz
          gunzip network-final.pkl.gz
          cd /stylegan2
          python run_metrics.py \
            --data-dir=/stylegan2/cat_images_tfrecords \
            --network=/ourTrainedNetwork/network-final.pkl \
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
      repo:
        type: volume
      ourTrainedNetwork: trainOurModel.outputs.ourTrainedNetwork
    outputs:
      generatedCatsOurs:
        type: dataset
        with:
          id: "dstba8lqk9g2x7v"
    uses: container@v1
    with:
      args:
        - bash
        - -c
        - |-
          pip install scipy==1.3.3
          pip install requests==2.22.0
          pip install Pillow==6.2.1
          cp -R /inputs/repo /stylegan2
          mkdir /ourTrainedNetwork
          cd /ourTrainedNetwork
          cat /inputs/ourTrainedNetwork/00000-stylegan2-cat-1gpu-config-f/network-final_* > network-final.pkl.gz
          gunzip network-final.pkl.gz
          cd /stylegan2
          python run_generator.py generate-images \
            --network=/ourTrainedNetwork/network-final.pkl \
            --seeds=6600-6605 \
            --truncation-psi=0.5 \
            --result-dir=/outputs/generatedCatsOurs
          ls "-aFlR" /outputs
      image: tensorflow/tensorflow:1.14.0-gpu-py3

```

