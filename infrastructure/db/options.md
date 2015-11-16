# Database Options

As with testing, exploring and comparing databases could fill a book of its own. This section will be a whirlwind tour of the current state of the world of databases.


## Relational Databases

Relational databases are so called because of the tabular way in which their data is stored. A *relation* is a table in which columns represent attributes, and each row is an *entity* with a value for each attribute. Invented in 1970 and used heavily ever since, relational database management systems (RDBMS) are among the most robust pieces of software.

There are three key characteristics of relational databases:

* **Schemas**: Each column (attribute) is well-defined by a *data schema*, and the values of each row must satisfy the constraints of the columns. Tabular schemas guarantee valid data, but can restrict the flexibility of the system.
* **Joins**: An operation known as a *join* is used to combine rows from different tables that share a common key. Joins are not inherently bad, but can become very expensive on very large datasets.
* **Transactions**: Relational databases perform write operations in *transactions*. Transactions have the [ACID properties][acid], which guarantee data is written reliably. This is often essential for working with mission-critical data, but it constrains how the database can be "scaled out".

The obvious relational DBaaS choice is the AWS **Relational Database Service** (RDS). RDS offers multiple relational databases, including MySQL, MSSQL, PostgreSQL and Amazon's own Aurora.


## NoSQL Databases

"NoSQL" has more or less come to mean "not relational". While perfect for many conventional use cases, relational databases struggle with others. The explosion of new software of unprecedented scale and complexity has given rise to a family of more specialised databases. This trend is summarised well by [Martin Fowler][mf] and [Pramod Sadalage][ps], and beautifully visualised by [451research][451].

The most common NoSQL databases include:

* **Key-Value** (Redis, Riak): Simple data structure optimised for massive throughput.
* **Document** (MongoDB, CouchDB): Hierarchical, flexible storage of complex data structures representing whole entities requiring fewer joins.
* **Column family** (Cassandra, HBase): Like a relational database thrown into a blender. Related columns are grouped for easier access, and each row can have different sets of columns. [Here's a nice illustration for Cassandra][colfam].
* **Graph** (Neo4j, Titan): Represents data as a graph of connected nodes. Extremely efficient for traversing relationships (relative to relational joins).

All of these NoSQL databases are designed to be run on a cluster of machines. This allows them to scale out and manage vast quantities of data with good performance.

Since there is such a large variety, I will focus only on [**MongoDB**][mongo]. MongoDB is perhaps the most popular, and its JSON API is well-suited for general-purpose, document-oriented Web apps.

AWS doesn't offer managed MongoDB-as-a-service, but there are three major players that do: [MongoLab][lab], [Compose.io](https://www.compose.io/) and [the MongoDB team](https://www.mongodb.com/cloud/). They all have the same API, but MongoLab has a free tier with 500 MB, so that's ideal for our experimentation.


## New Generation

With the rise of NoSQL and the explosion of Web apps, databases have become cool again. There are new databases being released seemingly every month with new features to trump the others.

Here's a list of new databases that I've heard good things about but haven't tried in practice:

* [**RethinkDB**](https://www.rethinkdb.com/): Like a real-time MongoDB, RethinkDB pushes changes to queries as they happen. This is very similar to the data model in [Meteor][meteor], which uses MongoDB's oplog and [tailable cursors][oplog].
* [**Firebase**](https://www.firebase.com/): More than just a a database, Firebase is an entire backend-platform-as-a-service. With Firebase you can build a real-time app with only front-end code.
* [**OrientDB**](http://orientdb.com/orientdb/): Combination of document and graph data models, promising the best of both worlds. Graph databases are greatly undervalued, so more options are always welcome.

If no single database is perfect, you can always use multiple. Each type of database can then store that kind of data it specialises in. This is known as [**polyglot persistence**][poly]. It can add substantial complexity, but also provide great benefits.

There are also some new query frameworks that have the potential to change the way databases are used (and hence chosen):

* [**GraphQL** and **Relay**][gqlrelay]: Facebook's smart data fetching language and framework. Built to implement the data flow pattern of [Flux][flux] for the [React][react] JavaScript UI library.
* [**TinkerPop**](http://www.tinkerpop.com/): A powerful framework for working with graph databases. In particular, [Gremlin traversals][gremlin] enable efficient graph exploration, with custom logic analogous to regular expressions.


## What should I do?

Given the almost unlimited choice, I'll assume for the sake of this book that you use [MongoDB][mongo] for your app and [MongoLab][lab] for DBaaS hosting. (MongoDB is the default for [Meteor][meteor], though support for others is gradually being added.)

1. Create an account for your organisation on MongoLab.
1. Create a user account for each DB admin that needs access. Add the admin users to the organisation account.
1. Create a new MongoDB deployment:
  * **Cloud provider​​**: AWS
  * **Location​​**: Your local AWS region
  * **Plan​​**: Single node > Sandbox
    * If Sandbox is not available, try the ​`us-east-1` region instead.
1. Select the database, and under the *Users* tab add a new database user with a username and password.

Take note of the Mongo URI, including the username and password of the new database user. We'll use that for [database integration](integration.md) in the next section.


[acid]: https://en.wikipedia.org/wiki/ACID
[mf]: http://martinfowler.com/articles/nosqlKeyPoints.html
[ps]: https://www.thoughtworks.com/insights/blog/nosql-databases-overview
[451]: https://451research.com/state-of-the-database-landscape
[colfam]: http://www.sinbadsoft.com/blog/cassandra-data-model-cheat-sheet/
[mongo]: https://www.mongodb.org/
[lab]: https://mongolab.com/
[poly]: http://martinfowler.com/bliki/PolyglotPersistence.html
[meteor]: https://www.meteor.com/
[oplog]: https://docs.mongodb.org/manual/tutorial/create-tailable-cursor/
[gqlrelay]: https://facebook.github.io/react/blog/2015/02/20/introducing-relay-and-graphql.html
[flux]: https://facebook.github.io/flux/docs/overview.html#content
[react]: https://facebook.github.io/react/
[gremlin]: https://tinkerpop.incubator.apache.org/docs/3.0.2-incubating/#_the_graph_process
