# ECS Task Definitions


## Container Definitions

A **container definition** is a template for a Docker container, just as a task definition is a template for tasks.

Quite simply, a container definition contains all of the arguments that you would pass to the `docker run` command. The first few are required, but most you can ignore. The most interesting options are:

* **Name**: Arbitrary, used for linking containers.
* **Image**: The Docker image to create the container from.
*  **Memory**: The maximum memory available to the container. If it needs more, it is killed.
   
   As a rule of thumb, consider giving each container slightly less than the amount of RAM per CPU core on the host. If all containers add up to the total of the host, there won't be enough left for the host itself.
*  **Port mappings**: Binding of ports inside the container to ports on the host.
   
   The most common use case is to bind the host's external port 80 (HTTP) to the application's port (e.g. 3000, 5000, 8080) in the container.
*  **CPU units**: The minimum CPU capacity that must be available for the container to be run (1 CPU = 1,024 CPU units).

   Note that containers are free to use more than this minimum if there is spare capacity. It should be barely enough for the application in the container to do its job.
* **Environment variables**:
* **Links**: A mechanism for containers to access each other without using explicit ports. Not necessary for simple applications, but a good feature to know about.
*  **Volume mount points**: A mechanism for persisting data when a container is terminated and restarted.

   This is essential for applications that store persistent data on disk (e.g. databases, WordPress, etc.). Containers may be restarted at any time, and without volumes, all internal state is reset.
