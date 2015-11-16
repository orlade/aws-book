# Continuous Integration (CI)

Like Agile software development, true continuous integration is easy to preach but challenging to practice. Even if everybody agrees it's a Good Thing, it still requires a daily commitment from everyone.

But what is Continuous Integration (CI)? There already exists an [excellent explanation by Martin Fowler][fowler], so I will summarise and focus on implementation.

* All developers synchronise (merge) their code frequently, at least one per day.
* Pushing code triggers an automated build and runs all tests.
* Build or test failures are visible to everyone and are fixed fast.

With the rise of cheap cloud computing infrastructure and virtualisation technologies such as Docker, there has been a rise in continuous integration services. Some well-known names are [Travis](https://travis-ci.org/), [Drone](https://drone.io/), [CircleCI](https://circleci.com/), [Codeship](https://codeship.com/) and [Shippable](https://app.shippable.com/).

**TODO**: Selection of CI tool

**Continuous delivery** is an extension of continuous integration. Delivery is the act of making new code available to users. Thus continuous delivery is the concept that every successful build is made available to customers immediately.


## What should I do?

**TODO**: Implementation details


[fowler]: http://martinfowler.com/articles/continuousIntegration.html
