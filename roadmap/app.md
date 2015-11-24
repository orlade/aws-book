# Application

This book is in part a guide. It describes how to set up a scalable AWS infrastructure to run a modern Web app. We'll be looking at one particular app: [**CloudChart**][website]. CloudChart is open-source, and you can [find the code on GitHub][repo].

CloudChart is, appropriately, an AWS infrastructure visualisation and monitoring app. It is built with the [Meteor framework](http://www.meteor.com/) on MongoDB for reactive GUI updating. Once it's deployed, you'll be able to visit it to see the infrastructure it's running on.

> **Info** CloudChart is available for you to explore, but still heavily under development and should not be considered ready for production use.

You can try out [a hosted instance of CloudChart][app]. The demo account will visualise the infrastructure that CloudChart is running on. If you're brave (or reckless) enough, you can provide your AWS access credentials to see your own cloud. Be aware that no security whatsoever is guaranteed.


## What should I do?

1. If you're not already a member of [GitHub](https://github.com/), sign up now.
1. [Fork CloudChart on GitHub][repo] so you can follow along with your own repository. `git clone` your new repository.
1. [Install Meteor](https://www.meteor.com/install) so you can run it locally.
1. In your cloned CloudChart directory, run `meteor` to start the app. Visit `localhost:3000` to check it out.

[website]: http://www.cloudchart.io
[repo]: https://github.com/orlade/cloudchart
[app]: http://app.cloudchart.io
