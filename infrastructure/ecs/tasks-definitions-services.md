# ECS Task Definitions, Tasks and Services

ECS has quite a convoluted conceptual model with a lot of terminology. Since it's based on Docker, it extends that vocabulary of images and containers with the following:

* A **?container instance** is an EC2 instance on which ECS will run Docker containers. It's just a plain EC2 instance with the ECS agent installed (included in [the ECS AMI we configured earlier](../ec2/launch-configurations.md)).
* A ?**cluster??** is a collection of container instances abstracted into a pool of resources (mostly CPU and RAM).
* A **?task??** is one or more containers that ECS deploys onto a single container instance. Tasks represent copies of your code running somewhere on an EC2 instance.
* A **?task definition??** is like a template for tasks. It groups one or more **container definitions**, which specify configurations for Docker containers. When a task is created from a task definition, a container is created from each container definition.
* A **?service??** is used to manage long­running tasks (like databases and web servers). It creates and maintains a given number of tasks, restarting them if they fail.

You can also run "once off" tasks (i.e. non-restarting) without a service. This is useful for some use cases, such as batch jobs. However most tasks will be run by services, so we'll focus on those.

It's a lot to get your head around, so let's walk through configuring each one.

## Cluster



## Task Definitions

Since [container definitions](container-definitions.md) are where the rubber meets the road, we discuss them in the next section.

## Services

[//]: (TODO: An ELB instance may be used to balance load across multiple tasks.)

## Tasks

You can see the tasks that are currently running under the Tasks tab of a cluster or a service. If services are managing your tasks, you shouldn't need to look at them unless something is wrong.

There is one exception, however: [updating](../../operations/updating.md). When you create a new revision of a task definition and update your service, the service will not automatically stop the old tasks and start new ones. Instead, you must manually stop the old tasks so new ones are automatically created using the new task definition.
