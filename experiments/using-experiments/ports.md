# Ports

### Why use ports?

Using port mapping enables you to access services running inside your Experiment remotely.   For example, you might want to run TensorBoard, [a simple flask web server](https://github.com/Paperspace/gradient-flask-example), or even [SSH directly into your running job instance](https://support.paperspace.com/hc/en-us/articles/360003413994).

![](https://support.paperspace.com/hc/article_attachments/360004109593/Screen_Shot_2018-04-23_at_9.34.32_AM.png)

### Opening Ports On Your Experiment

You can easily open ports into your Gradient Experiment using the `--ports` syntax.

If you are familiar with the Docker syntax for port forwarding, it is helpful to note that we use a similar form of:

```text
--ports $HOSTPORT:$CONTAINERPORT
```

For example, if you are running TensorBoard within your image and want to expose port 8888 to the world, you would just pass the following:

```bash
gradient experiment run ... --ports 8888:8888
```

