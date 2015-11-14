# ECS Clusters

A ?**cluster??** is a collection of container instances abstracted into a pool of resources (mostly CPU and RAM). There's not a lot to configure beyond a name, so let's talk about the **ECS agent**.

The ECS agent is a process that runs on each container instance of a cluster. It does three main jobs:

1. It registers the instance with the cluster.
2. It reports on how much capacity (CPU, RAM, etc.) is available on the instance.
3. It runs Docker containers when requested.
 
To register the instance with a cluster, it needs to know which cluster to register with. Registration happens when the instance boots up. The agent will register the instance with the cluster named in the instance's `CLUSTER` environment variable. If `CLUSTER` is not set, it will register with the `default` cluster.

## Why would I need multiple clusters?

For a simple app, the default cluster is fine. Every instance with the "ECS-Optimized Linux" AMI will register with it by default, and a service can schedule tasks onto any of those instances.

The problem occurs when you want to run two different tasks that would conflict if placed on the same instance. For example, if you had two public-facing 

The "correct" solution is to use multiple ELBs, each listening on port 80.
