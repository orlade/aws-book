# Simple Storage Service (AWS S3)

S3 is a simple service for working with files in the AWS cloud. They are easy to store, download, and control access to.

S3 stores files in collections called **buckets**. Each file is identified by a **key**, which looks like a regular file path. S3 has lots of cool features, but that's about all you need to know for now.

One good use case for S3 is to store confidential configuration files. These files can be read or copied from S3 by other AWS services to configure themselves without other AWS users needing access.

That's what we'll do here to store the [Docker Hub credentials we created before](../build/docker.md). This will be necessary for [ECS](../ecs/index.md) to pull private Docker images.


## What should I do?

1. Create a bucket in S3 for confidential system configuration scripts. The name doesn't matter, but it must be unique. Call it something like `<your name>-config`.
1. In that bucket, create a folder for your app.
1. In your new folder, create a subfolder called `ecs`. Replace the `<bracketed variables>` in the file below, and upload it as `ecs.config`:

  ```sh
ECS_ENGINE_AUTH_TYPE=docker
ECS_ENGINE_AUTH_DATA={"https://index.docker.io/v1/":{"username":"<agent username>","password":"<agent user password>","email":"<any@email.com>"}}
```

This may be a little confusing at the moment. It will make more sense once we've set up [EC2](../ec2/index.md) and [ECS](../ecs/index.md).
