# A Deployed Model's API Endpoint

#### Deployment states

When the deployment reaches the `running` state, it is available to make predictions.  See the full list of states [here](../deployment-states.md).

#### Endpoint URL

Once deployed, a secure URL will become available to make predictions.  This URL will be persisted until the deployment is deleted.  

#### Basic authentication

If basic authentication is enabled, the username and password must be passed-in with each request in order to reach the endpoint.  

#### Protocol

Gradient supports both REST and gRPC Deployment endpoints.  See [this article](https://docs.paperspace.com/machine-learning/wiki/rest-and-grpc) for more information on the differences.  

#### Load balancing

Incoming requests will be automatically load-balanced in a round-robin fashion if multiple instances are running.

