# Containers

All gradient resources use Docker containers to provide a code execution environment.

### Container Registries

Most mature organizations will host their Docker containers on private registries that require authorization. You can store credentials for future use in Gradient Resources through the **Containers** tab in your team settings.

![](<../.gitbook/assets/container-registry-create (1).png>)

A **Container Registry** is a url, namespace, username and password for the registry.

If you host your containers on Docker Hub your url would be `https://index.docker.io/v1/`, your repository would be your team's namespace like `paperspace` and your username and password are your login credentials. We suggest you use an Access Token as your password.

The url field supports an entire base url so you can use self-hosted options or cloud registries like GoogleContainerRegistry (GCR) that path mount your registry endpoint like `gcr.io/my-project`.

The `name` field is used to identify your registry in Paperspace resources and must be unique to your team.
