# Database Integration

Okay, so you've chosen a database and created an account with a DBaaS provider. Great job! Now you need to integrate that database with your application so you can start reading and writing data.

Compared to selecting and setting up the database, this is simple. All remote database servers will listen for connections and queries on a particular port. You just need to configure your application with the remote URL rather than the local one.

The queries your application makes (read and write) use an SDK to abstract whether your database is local or remote. Your database logic should not need to change!

One consideration to make is that network latency is orders of magnitude larger than local disk I/O, let alone memory. Thus the performance of your queries will be reduced when using a remote database relative to a local one. If this becomes a problem, try to reduce the number or size of the queries you make. If that's not enough, look into [replica sets][replica].


## What should I do?

Continuing with the assumption that you're using MongoDB and have set up an account with MongoLab:

1. Set the `MONGO_URL` environment variable to the Mongo URI from the [previous section](options.md), including the database user's username and password.
1. Run the application, read and write some data, and check that it is persisted in the DBaaS instance.

For now, you can just set the `MONGO_URL` variable manually. [ECS](../ecs/index.md) will let us declare all necessary environment variables more formally.


[replica]: https://docs.mongodb.org/manual/administration/replica-sets/
