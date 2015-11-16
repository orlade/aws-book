# Scalability

Scalability describes the volume of activity that a system is able to process. Activity is often measured in terms of concurrent users or size of data.

## Scaling Up

**Scaling up** means increasing the resources available per instance. In our case, this means replacing [EC2 instances](../infrastructure/ec2/instances.md) with more powerful instances (e.g. `c4` instances optimised for CPU speed).

Scaling up is usually easy to do without requiring any changes to the system architecture. However there is a limit to how far it can go (e.g. how fast a single CPU can get), and each step gets more expensive.

## Scaling Out

**Scaling out** means creating more instances and having them work together to share the load between them. In our case, we could stick with `t2.micro` instances, but just create twice as many to double the total resources available.

The potential of scaling out has much higher limits. For example, Google's infrastructure is based on the concept of huge volumes of commodity servers. The cost of scaling out also tends to increase in a more linear way.

## Considerations

The following considerations were made in the design of the system to allow it to be scaled out:

  * DBaaS instances are managed independently of the applications that use them.
    * Each DB will have a different load profile, which will also differ from the app. This design allows each to be scaled independently.
    * This also means the applications are essentially "stateless" (except for transient state like user sessions). Additional instances can be added and just as easily connected to the existing databases.
  * AWS is configured to support Auto Scaling.
    * The EC2 instance is provisioned by an [Auto Scaling Group](../infrastructure/ec2/auto-scaling-groups.md) (ASG). Additional copies of that instance can be created by simply editing the ASG.
    * The application is provisioned into an [ECS cluster](../infrastructure/ecs/clusters.md), which abstracts the EC2 instances. Additional (or larger) EC2 instances provisioned via the ASG will be automatically added to the cluster.
    The [ECS service](../infrastructure/ecs/tasks-services.md) can be edited the same was as the ASG to deploy more instances of the application.
