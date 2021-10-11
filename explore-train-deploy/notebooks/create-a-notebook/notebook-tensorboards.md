# Notebook TensorBoards

To run Tensorboard in a notebook open a notebook terminal using the Terminal button and run:
```
tensorboard --logdir . --bind_all
```
(Change the `--logdir` path to a different value if needed.)

You can then access the Tensorboard via this URL scheme `https://tensorboard-NOTEBOOKID.CLUSTERID.paperspacegradient.com`

The NOTEBOOKID can be found on the notebook list view.

The default CLUSTERID is `clg07azjl`. \(If using a private cluster, you can grab the CLUSTERID from the clusters page.\) 

You can also get the NOTEBOOKID and CLUSTERID from the url provided by the Jupyter button on the notebook page. Right-click on the Jupyter button and copy the link, then pre-prend `tensorboard-` in front of the NOTEBOOKID and remove the `/token=...` path and query variable from the end.
     
Here’s an example:

![](https://s3-ap-southeast-1.amazonaws.com/blob.blankcursor.com/uploads/editor_attachment/attachment/5650/792a03f09ffcf0db65f4f6fccfe20e561571de8d_2_1117x586.png)

Inside the container, the default port of 6006 should still be used.

