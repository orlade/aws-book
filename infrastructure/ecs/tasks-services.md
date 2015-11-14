# ECS Tasks and Services

## Tasks

You can see the tasks that are currently running under the Tasks tab of a cluster or a service. If services are managing your tasks, you shouldn't need to look at them unless something is wrong.

There is one exception, however: [updating](../../operations/updating.md). When you create a new revision of a task definition and update your service, the service will not automatically stop the old tasks and start new ones. Instead, you must manually stop the old tasks so new ones are automatically created using the new task definition.

## Services

[//]: (TODO: An ELB instance may be used to balance load across multiple tasks.)
