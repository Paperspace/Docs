# Distributed Training

Gradient supports distributed training via two powerful options: gRPC and MPI.

As a messaging protocol, gRPC distributed training can be used with both TensorFlow and PyTorch. gRPC for TensorFlow is supported natively, while gRPC for PyTorch will require some manual setup.

{% page-ref page="multi-node-training.md" %}

{% page-ref page="distributed-machine-learning-with-mpi/" %}



