# EC2 Auto Scaling Groups

Auto Scaling is a feature of EC2 that can automatically adjust the capacity of your system. It does this by creating and terminating EC2 instances.

In particular, which the load on your system increases, new instances are created to share the load. When that load decreases, the excess instances are terminated to save money.

An **Auto Scaling Group** (ASG) is used to configure this feature. In the ASG, you specify three main things:

1. The minimum and maximum number of [EC2 instances](instances.md) that should be running at any time.
2. The [Launch Configuration](launch-configurations.md) to use when creating new instances.
3. The [Elastic Load Balancer](elastic-load-balancers.md) that new instances should be registered with.

As you can see, Auto Scaling Groups really tie the EC2 features together.

## What should I do?

1. Create a new Auto Scaling Group.
1. Configure it with an existing [Launch Configuration](launch-configurations.md).
1. Select all default subnets.
1. In Advanced Details, check "Receive traffic from Elastic Load Balancer(s)" and select your [Elastic Load Balancer](elastic-load-balancers.md).
1. Select "Use scaling policies to adjust the capacity of this group", with the following policies:
   * Scale between 1 and 3 instances (or however many you're comfortable with)
   *  **Increase group size**: Add new alarm (as below), and take the action "Add 30 percent of group"
      ![Configuration of CloudWatch alarm triggering an auto scale out][increase]
   *  **Decrease group size**: Add new alarm (as below), and take the action "Remove 2 instances"
      ![Configuration of CloudWatch alarm triggering an auto scale in][decrease]
1. Ignore notifications and tags.
1. Review and create the ASG.

Finally, your EC2 service is capable of creating its own instances as needed!

## What's Next?

Thanks to the AMI and User Data added in the [Launch Configuration](launch-configurations.md), each instance will automatically join an [ECS cluster](../ecs/clusters.md). While EC2 manages the infrastructure your applications run on, ECS manages what applications are running. This is a powerful [separation of concerns][soc].

This wraps up our configuration of EC2, so let's [move right along to setting up ECS](../ecs/index.md)!

## See Also

* [AWS Auto Scaling tutorial][tutorial]

[tutorial]: https://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/as-register-lbs-with-asg.html
[increase]: https://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/images/as-console-create-scaleout-policy.png
[decrease]: https://docs.aws.amazon.com/AutoScaling/latest/DeveloperGuide/images/as-console-create-scalein-policy.png
[soc]: https://en.wikipedia.org/wiki/Separation_of_concerns
