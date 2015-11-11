# ECS Tasks and Services

**Tasks** are ECS resources that run containers (which in turn run your code). **Services** are ECS resources that run tasks, and restart them if they fail.


## Tasks

Tasks are created from task definitions. The task will create a configured container from each container definition in the task definition. Docker images are built ready to run, so the simple act of running a container will do the task's job.


## Services

A **service** has two jobs: create tasks and keep them running.

A service is configured with a specific revision of a task definition and a desired number of tasks. It will create that many tasks from the task definition and monitor their status. If one of the tasks stops, it will automatically start a new one to replace it.

A service may also be configured with an [ELB](../ec2/elastic-load-balancers.md) (if one has been created). Whenever the service creates a task, its container instance will be registered with the ELB so ELB traffic is directed to it.


## Maintenance

You can see the tasks that are currently running under the Tasks tab of a cluster or a service. If services are managing your tasks, you shouldn't need to look at them unless something is wrong.

There is one exception, however: [updating](../../operations/updating.md). When you create a new revision of a task definition and update your service, the service will not automatically stop the old tasks and start new ones. Instead, you must manually stop the old tasks so new ones are automatically created using the new task definition.


## What should I do?

1. Select a cluster.
1. Create a new service.
1. Select your task definition and its latest revision.
1. Give the service a name, and request 1 task.
1. Select your ELB.
1. Watch the service for a couple of minutes to ensure it starts successfully.
1. Visit the ELB's IP address. You should see your app running!
