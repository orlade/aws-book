# EC2 Container Service (AWS ECS)

ECS is the most complicated component of this system. It's also the most rewarding.

We talked about Docker, and how it abstracts away the specifics of the host machine. However, the machine must still exist. Then we spoke about EC2 and how it can automatically create virtual machines to spec. However, we still need to log into those individual machines to deploy our application.

ECS provides another layer of abstraction: the **cluster**. An ECS cluster manages a collection of EC2 instances as a pool of resources. This means we don't need to access them individually. This is possible because every instance in the cluster has a common factor: Docker.

With EC2, we manually deploy application code onto an operating system and run it. With ECS, we just ask it to deploy a Docker container wherever there is space. The general purpose EC2 instances are reduced to simple Docker Machines, which require virtually no maintenance. All that good work we've put into the underlying infrastructure means we will barely need to think about it again!

But we're not there yet. ECS still needs to be configured. It has quite a complicated conceptual model, and there are plenty of gotchas along the way. Let's get to work!
