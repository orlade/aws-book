# Elastic Compute Cloud (AWS EC2)

EC2 provisions and configures virtual machines (VMs) called [**instances**](instances.md). Instances are essentially just computers, and they can do anything a computer can do. In your technical infrastructure, they are the workhorses that sit and run your code 24 hours a day.

EC2 is more than just instances, however. It also includes a handful of services that manage those instances. Since instances are so general-purpose, there are many configuration options available. These include operating system, performance/price tradeoffs, and [Security Groups](security-groups.md).

When you launch a new instance, you must set values for these options. If you plan to have multiple instances doing the same thing, you can create a [Launch Configuration](launch-configurations.md) which can then be used to create multiple identical instances. Furthermore, an [Auto Scaling Group](auto-scaling-groups.md) can automatically create more instances if the load on your system increases.

Each instance receives an IP address, which can be used to connect to it. When [scaling out](../operations/scaling.md) a system, there will be multiple instances, each with different IP addresses. An [Elastic Load Balancer](elastic-load-balancers.md) distributes requests to a single IP address across multiple instances.

Let's walk through each of these features in a little more detail and set them up.
