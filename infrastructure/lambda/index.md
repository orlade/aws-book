# AWS Lambda and API Gateway

Lambda is a relatively new service from Amazon with a lot of potential. In summary, it executes snippets of code on demand, completely abstracting the infrastructure on which they are run.

## Lambda

This makes it an ideal for triggering actions in response to relatively infrequent events. Examples of prime use cases are:

* Infrequent user actions, such as exporting application data.
* Running scheduled tasks.
* Adjusting infrastructure in response to metrics such as CPU load.

For our continuous delivery process, the latter is of interest. EC2 Auto Scaling is great, but it doesn't do everything:

* EC2 can automatically adjust the number of instances.
* ECS can automatically provision a given number of tasks onto those instances.
* However ECS does not have an Auto Scaling capability to automatically adjust the number of desired tasks.

Thus we can use Lambda to respond to AWS CloudWatch alarms and adjust the number of ECS tasks the same way that Auto Scaling adjusts the number of EC2 instances. In addition, ECS task definitions and services must be updated manually when new versions of code are available. Lambda can automate this process through the AWS API.


## API Gateway

Lambda abstracts the infrastructure required to run snippets of code. **API Gateway** abstracts the infrastructure (and code) needed to define a RESTful API and receive and delegate HTTP requests.

This could be useful for implementing your application's API, but that will usually be an integral part of the application code. However, API Gateway is ideal for implementing auxiliary APIs to support your application. For example, it makes it very easy to handle webhooks from other services.

API Gateway provides many features to define the API, but ultimately it delegates the request to another service. The simplest form of delegation is to trigger a Lambda function, which can in turn trigger other services.

In this case, we want to trigger an ECS auto-scaling Lambda function in response to the completion of a new build on Docker Hub.

> **Warning** API Gateway methods can be secured, but must be public to work with webhooks. Public method can be called by anyone who knows the URL. Thus your Lambda function must verify whether its action should be performed before executing it.


## What should I do?

1. Create a Lambda function to perform an ECS update. Given a new Docker image tag:
  1. For each ECS task definition that uses the image, create a new revision that uses the new tag.
  1. For each ECS service that uses the previous revision of the task definition, update it to use the new revision.
  1. Update the existing ECS tasks created by the service using the old revision. Simply stopping the tasks will cause the service to recreate them. However ECS may also perform a rolling update if there is sufficient capacity available.
1. Create an API Gateway endpoint to invoke the Lambda function.
1. Register the endpoint as a Docker Hub webhook. The Lambda function will be invoked whenever a Docker Hub build finishes.
