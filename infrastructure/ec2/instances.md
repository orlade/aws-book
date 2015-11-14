# EC2 Instances

An EC2 instance is a virtual machine (VM) running in the cloud. Ultimately there is a physical machine in a data centre somewhere running the VM, but this is not important. Cloud computing means we care only about function, not form.

## Instance Types

An EC2 **instance type** is a hardware configuration that determines the instance's performance, capacity and cost. EC2 instances [come in many shapes and sizes][types], but they boil down to just a few points:

* `m4` types are powerful general purpose instances. You can basically use these for everything.
* `t2` types are similar, except they are smaller and cheaper, and even cheaper still when they are idle.
* `c`, `r`, `g`, `i` and `d` types specialise in CPU speed, RAM capacity, GPU power, storage I/O (SSD) and storage capacity (HDD) respectively. You probably don't need them.

Once you choose a type, you can choose a size. This determines the number of CPU cores, amount of RAM, etc. A decent, cost-effective rule of thumb is one CPU core per application you're running. The `t2.micro` is a good choice for experimenting, so start with that until you need more. Better yet, for your first 12 months you get a single `t2.micro` instance on the [AWS Free Tier][free]. Score!

Speaking of cost savings, there's three different payment plans for EC2 instances:

* **On-Demand**: Pay per hour of use. Nice and easy.
* **Reserved Instance**: Pay a deposit up-front, and a reduced rate per hour of use. Larger deposit => smaller hourly rate. This can be great if you're planning 1-3 years into the future.
* **Spot Instance**: Pay a rate per hour of use that fluctuates with spot instance market demand. The rate is usually quite stable at about 10% of the On-Demand rate, but can spike to multiple times higher. You submit a maximum bid, and if the market rate exceeds that, your instance is terminated. Spot instances can be extremely cost effective, but are more complex to manage.

[//]: # (TODO: Table of instance prices for common use cases)

## What should I do?

Nothing yet!

Launching an instance is easy enough, but you have to wade through pages of configuration. We'll discuss the options in the next section. Once a launch configuration is defined, we want EC2 to launch our instances automatically.

By the end of the chapter, we'll have a miniature fleet of two instances that can be expanded at will. It'll be worth the wait. But if you really want, you can launch a `t2.micro` instance manually to get a feel for it. Here's where it fits into the architecture:

![System architecture diagram with a single instance](../images/arch-single-instances.png)

[types]: https://aws.amazon.com/ec2/instance-types/
[free]: https://aws.amazon.com/free/
