# Deployment Spec

A deployment is maintained by a spec file which is used to change the state of the deployment.

```yaml
image: lucone83/streamlit-nginx # container image used to run your deployment
command: # optional command to override the container image's default command
  - my
  - command
port: 8080 # local container port that your service is running on
env: # environment variables that are applied at run time
  - name: ENV
    value: VAR
resources:
  replicas: 1 # number of replicas used for your deployment
  instanceType: C3 # instance type that your deployment will run on
```

