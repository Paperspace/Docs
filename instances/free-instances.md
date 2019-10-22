# Free Instances \(Free Tier\)

### About

Gradient offers a Free Tier of free GPU and CPU instances, available to all users of [Gradient Community Notebooks](../notebooks/public-notebooks.md) \(currently in beta\).

The Free Instances are available to all _Private Workspace_ plans, i.e. G\* subscriptions \(not T\*\). 

### Instance Types available in the Free Tier

**Free-CPU** — C3 CPU instance

**Free-GPU+** — NVIDIA M4000 GPU

**Free-P5000** — NVIDIA P5000 GPU

See the [Instance Types](instance-types.md) page for the details on these instances.

### Persistent Storage for Free Instances

For your machine learning work on Free Instances, you have 5GB of dedicated Persistent Storage. This 5GB of storage is dedicated and persistent regardless of which Private Workspace subscription plan you're on.

Because Persistent Storage is exclusive per-region, this means that data in Persistent Storage for the Free Tier is not be accessible from paid instance types, and vice versa.

For example, you can be on a G2 subscription plan with 1TB of Persistent Storage, which will be used for your paid work, and any Free Instances that you use \(which you will still have access to\) will still use their dedicated 5GB of persistent storage.

### Limits of Free Instances

All free instances have the same limits, regardless of your subscription plan:

* Notebooks will automatically shutdown after 6 hours per session
  * There are currently no limits to the number of sessions you can run
* All Notebooks \(and Jobs coming soon\) will be set to public and cannot be set to private
* 5GB of [persistent storage](../data/storage.md#persistent-storage) is included for free — this cannot be expanded

_Note: We are currently offering a limited pool of free instances so your notebook may be Pending in the queue as you wait for a free instance to become available. If you need immediate access to machines, please consider upgrading to a paid subscription plan._

\_\_

\_\_

