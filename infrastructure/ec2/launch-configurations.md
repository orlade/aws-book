# EC2 Launch Configurations

Launching an EC2 instance requires a large number of options to be set. A **launch configuration** is a collection of settings from which a new instance can be launched with a single click.

Launch configurations make it easier to launch an instance manually, but more importantly they allow EC2 to launch instances automatically. This is a key requirement for [Auto Scaling](auto-scaling-groups.md), which is the ultimate goal of the service.


## User Data

One particularly important configuration is the instance's "User data" (in Advanced Details). The content of this property is executed when the instance is *created* (i.e. on the first boot, and never again). Since the instances will be automatically created, this is your only chance to customise the base operating system.

There are a couple of ways to run logic every time the system boots (e.g. to set environment variables):

* Append the logic to `~/.bashrc`.
* Write the logic to a script and add it to `cron` as a `@reboot` task.
* Write the logic somewhere that a service expects to find it.

In our case, we want to store our Docker credentials somewhere on the machine so that ECS can pull private images. ECS runs an agent on the instance, and that agent executes `/etc/ecs/ecs.config` every time it starts. Thus we can use the latter option above.

In previous steps, we've configured an [IAM role with S3 read access](../iam/roles.md), and we've created [a config file with our Docker credentials in a private S3 bucket](../s3/buckets.md). Thus, after it is created, the instance (with the role) will be able to copy the ECS config file into the ECS agent's path, and all will be configured.


## What should I do?

1. Create a launch configuration to specify the kind of instance you want your application to run on.
1. Search the AWS Marketplace for the ["Amazon ECS-Optimized" AMI][ami] and select it.
1. Select the instance type you want (`t2.micro` unless you need something bigger).
1. Set the IAM role to the `ecsInstanceRole` [we created earlier](../iam/roles.md).
1. Set the "User data" to:

   ```sh
#!/bin/bash
yum install -y aws-cli
aws s3 cp s3://crcsi-config/rezone/ecs/ecs.config /etc/ecs/ecs.config
echo "
ECS_CLUSTER=<app name>" >> /etc/ecs/ecs.config
   ```
1. Use the default storage.
1. Select the [security group we created previously](security-groups.md).
1. Review and create the launch configuration.


[ami]: https://aws.amazon.com/marketplace/pp/B00U6QTYI2
