# Ports

### Why use a public IP?

Public IP addresses are useful for accessing your Gradient job container from the outside world. For example, you might want to run TensorBoard, [a simple flask web server](https://github.com/Paperspace/gradient-flask-example), or even [SSH directly into your running job instance](https://support.paperspace.com/hc/en-us/articles/360003413994).

Gradient Notebooks and Jobs automatically have public IP addresses. For Jobs, you can additionally pass in which ports you would like to open on the running Job.

![Ports may be specified for each job](../../.gitbook/assets/screen-shot-2021-01-18-at-10.08.45-pm.png)

### Opening Ports On Your Job

You can easily open ports into your Gradient job using the --ports syntax.

If you are familiar with the Docker syntax for port forwarding, it is helpful to note that we use a similar form of:

```text
--ports $HOSTPORT:$CONTAINERPORT
```

For example, if you are running TensorBoard within your image and want to expose port 8888 to the world, you would just pass the following:

```text
gradient jobs create --container tensorflow/tensorflow:latest --command './run.sh' --ports 8888:8888
```

Within the interface you can see that this job has the public IP address of 104.196.249.111, so now any traffic that you send through 104.196.249.111:8888 will get redirected to the job's container on that same port.

![Screen\_Shot\_2018-04-23\_at\_9.17.59\_AM.png](https://support.paperspace.com/hc/article_attachments/360004083894/Screen_Shot_2018-04-23_at_9.17.59_AM.png)

### Considerations / Additional Notes

Public IP addresses are not persistent. This means that once a job terminates, the public IP address is released back into the pool and is no longer available.  

