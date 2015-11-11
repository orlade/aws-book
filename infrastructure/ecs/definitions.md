# ECS Task and Container Definitions

Task and container definitions are templates from which task and containers are created. They contain the settings with which new tasks and containers are configured. This is similar to the [Launch Configurations](../ec2/launch-configurations.md) in EC2, from which new instances are created.

To recap, a container is a lower-level isolated environment in which your code is executed. A task is a higher-level ECS resource that runs one or more containers.


## Task Definitions

A **task definition** contains all the information required to run a task. This includes one or more container definitions and optionally some volumes to store container data.

Tasks group multiple containers and volumes in order to configure relationships between them. Task *definitions* are groups of *definitions* of these containers and volumes. Typical relationships include:

* Ensuring two containers are placed on the same instance and both running at the same time.
* Linking containers to provide more direct access.
* Associating a volume with one or more containers.

In practice, it is very common for a task definition to have a single container definition with a list of environment variables and no volumes.

Once a task definition is saved, every set of changes you make to it requires a new **revision**. The name of the task definition is actually a **family** of task definitions. Tasks are created from a specific revision within a family.


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
* **Environment variables**: Variables that will be set in the container environment. Your applications can read these at runtime. A key component of a [12 Factor app][12fa-config]. 
* **Links**: A mechanism for containers to access each other without using explicit ports. Not necessary for simple applications, but a good feature to know about.
*  **Volume mount points**: A mechanism for persisting data when a container is terminated and restarted.

   This is essential for applications that store persistent data on disk (e.g. databases, WordPress, etc.). Containers may be restarted at any time, and without volumes, all internal state is reset.

## What should I do?

1. Create a new task definition.
1. Add a container definition.
   * Name it after your application.
   * Set the image to `<your Docker username>/<your Docker image name>:<optional Docker tag>`.
   * Set the memory to 900 MB (all instance types have at least 1 GB RAM per CPU core).
   * Map host port 80 to container port 3000 (or whatever port your app binds to).
1. Save the container and task definitions.

[12fa-config]: http://12factor.net/config
