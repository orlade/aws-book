# Application

This book is in part a guide. It describes how to set up a scalable AWS infrastructure to run a modern Web app. So that we're on the same page, the book will describe the deployment of one particular app: [**Cortex**][repo].

> **Info** Cortex has not been released yet, but a very early version will be very soon.

Cortex is, appropriately, an AWS infrastructure monitoring app. It is built with the [Meteor framework](http://www.meteor.com/) on MongoDB for reactive GUI updating. Once it's deployed, you'll be able to visit it to see the infrastructure it's running on.

Cortex requires the following environment variables to be set:

* `METEOR_ADMIN_EMAIL`
* `METEOR_ADMIN_PASSWORD`
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`

**TODO**: Details.


## What should I do?

1. If you're not already a member of [GitHub](https://github.com/), sign up now.
1. [Fork Cortex on GitHub][repo] so you can follow along with your own repository. `git clone` your new repository.
1. [Install Meteor](https://www.meteor.com/install) so you can run it locally.
1. In your cloned Cortex directory, run `meteor` to start the app. Visit `localhost:3000` to check it out.

[repo]: https://github.com/orlade/cortex
