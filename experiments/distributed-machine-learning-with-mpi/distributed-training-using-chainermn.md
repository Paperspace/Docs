---
description: ChainerMN enables multi-node distributed deep learning
---

# Distributed Training Using ChainerMN

[This blog post](http://chainer.org/general/2017/02/08/Performance-of-Distributed-Deep-Learning-Using-ChainerMN.html) provides  benchmark results using up to 128 GPUs.

ChainerMN can be used for both inner-node \(i.e., multiple GPUs inside a node\) and inter-node settings. For inter-node settings, we highly recommend to use high-speed interconnects such as InfiniBand.

ChainerMN examples are available on [GitHub](https://github.com/chainer/chainer/tree/master/examples/chainermn/). These examples are based on the [examples of Chainer](https://github.com/chainer/chainer/tree/master/examples/) and the differences are highlighted.





