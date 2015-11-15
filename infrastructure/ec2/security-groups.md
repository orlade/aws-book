# EC2 Security Groups

**Security groups** are like firewalls: they are a set of rules that restrict network access to EC2 instances. It is good practice in security to block any access that is not strictly necessary.

Each rule allows traffic of a certain protocol to one or more ports from certain sources. Rules are quite configurable, but in most cases only a few simple rules are needed:

| Type       | Protocol | Port Range | Source    |
| ---------- | -------- | ---------- | --------- |
| SSH        | TCP      | 22         | 0.0.0.0/0 |
| HTTP       | TCP      | 80         | 0.0.0.0/0 |
| HTTPS      | TCP      | 443        | 0.0.0.0/0 |
| Custom TCP | TCP      | 3000       | 0.0.0.0/0 |

* SSH access allows you to login to your instance manually. This is usually a given for typical EC2 use. However when using ECS, it's not strictly necessary (though still useful for debugging errors).
* HTTP and HTTPS allow browsers to connect directly to the instance via its IP address. When using an [ELB](elastic-load-balancers.md), this is not necessary since the ELB will forward HTTP(S) ports to your application's port.

By the end of this book, ELBs will be the only Internet-connected instances, and ECS will manage everything that runs on the instances. Thus the most restrictive security group will allow only TCP connections to the application's port.

Note that Security groups can also restrict outbound traffic, but this is not usually necessary.


## What should I do?

1. Create a security group.
1. Create a single rule allowing inbound TCP access to only your application's port (3000) from Anywhere.
1. Save the security group.
