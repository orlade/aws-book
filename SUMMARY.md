# Summary

* [Introduction](README.md)
* [Objectives](objectives.md)
* Roadmap
   * Application (Meteor)
   * Services
* [Build](build/index.md)
   * [Source Code Management (Git)](build/scm.md)
   * [Virtualisation (Docker)](build/virtualisation.md)
   * [Automated Testing](build/testing.md)
   * [Continuous Integration (CI)](build/ci.md)
* [Infrastructure](infrastructure/index.md)
   * Database Management
       * Database-as-a-Service (DBaaS)
       * Relational Database Service (AWS RDS)
       * MongoDB
   * Identity and Access Management (AWS IAM)
       * Permissions
       * Users, Groups and Roles
       * [Certificates](infrastructure/iam/certificates.md)
   * [Simple Storage Service (AWS S3)](infrastructure/s3/index.md)
   * [Elastic Compute Cloud (AWS EC2)](infrastructure/ec2/index.md)
       * [EC2 Instances](infrastructure/ec2/instances.md)
       * [Security Groups](infrastructure/ec2/security-groups.md)
       * [Launch Configurations](infrastructure/ec2/launch-configurations.md)
       * [Elastic Load Balancers](infrastructure/ec2/elastic-load-balancers.md)
       * [Auto Scaling Groups](infrastructure/ec2/auto-scaling-groups.md)
   * [EC2 Container Service (AWS ECS)](infrastructure/ecs/index.md)
       * [Terminology](infrastructure/ecs/terminology.md)
       * [Clusters](infrastructure/ecs/clusters.md)
       * [Task and Container Definitions](infrastructure/ecs/definitions.md)
       * [Tasks and Services](infrastructure/ecs/tasks-services.md)
* Presentation
   * Static Website Hosting
       * Static Site Generation (Jekyll)
       * Hosting and Deployment (AWS S3)
   * Domain Name Service (AWS Route 53)
       * Hosted Zones and Record Sets
       * Subdomains
* Operations
   * Updates and Rollbacks
   * Backups
   * Scaling
   * Debugging
* Quality Attributes
   * Security
   * Scalability
   * Cost
* Modern Deployment Cheat Sheet
