# ECS Terminology

ECS has quite a convoluted conceptual model with a lot of terminology. Since it's based on Docker, it extends that vocabulary of images and containers with the following:

* A **container instance** is an [EC2 instance](../ec2/instances.md) on which ECS will run Docker containers. It's just a plain EC2 instance with the ECS agent installed (included in [the ECS AMI we configured earlier](../ec2/launch-configurations.md)).
* A [?**cluster??**](clusters.md) is a collection of container instances abstracted into a pool of resources (mostly CPU and RAM).
* A [**?task??**](tasks-services.md) is one or more containers that ECS deploys onto a single container instance. Tasks represent copies of your code running somewhere on an EC2 instance.
* A [**?task definition??**](definitions.md) is like a template for tasks. It groups one or more [**container definitions**](definitions.md), which specify configurations for Docker containers. When a task is created from a task definition, a container is created from each container definition.
*  A [**?service??**](tasks-services.md) is used to manage long­running tasks (like databases and web servers). It creates and maintains a given number of tasks, restarting them if they fail.

   You can also run "once off" tasks (i.e. non-restarting) without a service. This is useful for some use cases, such as batch jobs. However most tasks will be run by services, so we'll focus on those.

It's a lot to get your head around, so we'll walk through them in the following sections.


