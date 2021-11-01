# Free Instances (Free Tier)

## About

Gradient offers a Free Tier of free GPU and CPU instances, available to all users of [Gradient Community Notebooks](../../explore-train-deploy/notebooks/create-a-notebook/public-notebooks.md) (currently in beta).

The Free Instances are available to all _Private Workspace_ plans, i.e. G\* subscriptions (not T\*).

## Instance Types available in the Free Tier

**Free-CPU** — C4 CPU instance

**Free-GPU+** — NVIDIA M4000 GPU

**Free-P5000** — NVIDIA P5000 GPU (requires G1 or great subscription [plan](https://gradient.paperspace.com/pricing))&#x20;

See the [Instance Types](./) page for the details on these instances.

## Persistent Storage for Free Instances

For your machine learning work on Free Instances, you have 5GB of dedicated Persistent Storage. This 5GB of storage is persistent and upgradeable based on your subscription tier.

Because Persistent Storage is exclusive per-region, this means that data in Persistent Storage for the Free Tier is not accessible from paid instance types, and vice versa. However, you may upgrade the storage size of your Free Tier instances based on paid subscription storage sizing.

For example, you can be on a G2 subscription plan with 1TB of Persistent Storage, which will be used for your paid work, and any Free Instances that you use (which you will still have access to) will also have access to their dedicated 1TB of persistent storage. This storage, however, cannot be shared between instance types.

## Limits of Free Instances

All free instances have the same limits except for persistent storage, regardless of your subscription plan:

* Notebooks will automatically shutdown after 6 hours per session
  * Only 1 Free Notebook can be run at a time&#x20;
* All Notebooks will be set to public and cannot be set to private

_Note: We are currently offering a limited pool of free instances so your notebook may be Pending in the queue as you wait for a free instance to become available. If you need immediate access to machines, please consider upgrading to a paid instance type._
