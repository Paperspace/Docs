# Container Management

Whether you are using Notebooks, Workflows or Deployments, Gradient uses containers to provide a code execution environment that allows you to interact with all resources.&#x20;

In the case of notebooks, you can either use a preconfigured container or bring your own container. To learn more about that see the [Notebook containers page](../explore-train-deploy/notebooks/create-a-notebook/notebook-containers/).

For Workflows and Deployments, you can either use public containers or private containers to set up your environment. With public containers (for example [`tensorflow/tensorflow:2.7.0-gpu-jupyter`](https://hub.docker.com/r/tensorflow/tensorflow/tags) if you wanted to use a generic Tensorflow environment) then Gradient takes care of everything once you specify that in the `image` for your workflow. Learn more about workflow specs on the [getting started with workflows page](../explore-train-deploy/workflows/getting-started-with-workflows.md).

You can also use a private container in your Workflows and Deployments. Gradient makes it easy for you to store and manage your private registry credentials which you can learn more about below.

### Container Registries

You can store credentials for future use in Gradient Resources through the **Containers** tab in your team settings. Access your team settings by clicking on your user image in the top right of the console.

Within the Containers tab you can add new container registries as well as edit or delete your existing registries.

![Container Tab](<../.gitbook/assets/Screen Shot 2022-01-20 at 9.16.02 PM.png>)

#### **Creating a new Container Registry Entry**

To create a new container registry, simply click the **Add a New Container Registry** button to get the entry form that will allow you to enter in the following information:

![New Container Registry](<../.gitbook/assets/container-registry-create (1).png>)

* `name` - This field is used to identify your registry in Paperspace resources and must be unique to your team.
* `url` - The url associated with the registry hosting the container. For example, If you host your containers on Docker Hub your url would be `https://index.docker.io/v1/`. This supports an entire base url so you can use self-hosted options or cloud registries like GoogleContainerRegistry (GCR) that path mount your registry endpoint like `gcr.io/my-project`.
* `namespace` - This is the unique location within your registry outlining the loaction of your repository inclusive of namespace, sub-namespaces and tag.

![Registry url and Namespace Example](<../.gitbook/assets/Screen Shot 2022-01-20 at 9.58.00 PM.png>)

* `username` - This is your username login credential for the registry.
* `password` - This is your password login credential for the registry. It is suggested you use an Access Token as your password.

Check this out to learn more about [docker registries](https://docs.docker.com/get-started/overview/#docker-registries).



