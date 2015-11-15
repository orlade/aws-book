# Testing

Testing is how you (attempt to) ensure that your code does what you expect under a variety of circumstances. At the highest level, there are two main kinds of testing:

* **Manual testing** is performed by humans interacting with the application as a user would.
* **Automated tests** is executed by the computer given precise setup and expectations by the developer.

Both should be performed regularly, but automated testing should be preferred. The advantage of automated tests is that they are very mechanical. This means computers can run a large volume of them very frequently. It also means that once a bug is tested and fixed, it will be discovered immediately if it comes back again (known as a "regression").


## Build Process

Suffice it to say that testing is a field of its own with immense depth. What we're interested in here is how it affects the build and deployment processes.

Automated testing should definitely be used as part of the build process. In particular, the build process should require **all** automated to pass before the build is successful and can be deployed. We'll explore the mechanics of that in the next section on [continuous integration](ci.md).

For now, the most important thing is that there are automated tests to run. There are many different kinds of automated test. To get the most assurance bang for your development buck, focus on two of them:

*  **Unit tests** examine the behaviour of the smallest units of code: individual functions. When different sets of arguments go in, the expected results should come out.

   Ideally every function would have unit tests, although this is often impractical. Try to at least write unit tests for really easy functions (simple input/output) and really complicated functions (difficult to reason about by inspection).

* **End-to-end tests** (or system tests) examine the behaviour of the entire integrated system from the user's perspective. The tests simulate user inputs and observe the outputs that would be displayed to the user.

To measure your progress, it is very motivating to set up test coverage analysis. This calculates (among other things) what percentage of the lines of code were executed *at least once* by any test. Ideally this should be 100%. This is especially important for dynamically typed languages like JavaScript and Python, where any un-executed line of code could contain fatal syntax errors.


## What should I do?

These steps assume a Meteor application. Other applications will be similar, and may even use some of the same libraries.

1. Run `meteor add sanjo:jasmine xolvio:cucumber velocity:html-reporter`.
1.  Create a new test specification in the project root `/tests/jasmine/server/unit/MyClassSpec.js`:

   ```js
   describe('MyClass', function () {
     'use strict';

     beforeEach(function () {
       MeteorStubs.install();
       mock(global, 'Players');
     });

     afterEach(function () {
       MeteorStubs.uninstall();
     });

     describe('getPlayerList', function () {
       it('should ask for the players in primarily in descending score order, then in alphabetical order and return them', function () {
         var result = {};
         spyOn(Players, 'find').and.returnValue(result);
         expect(PlayersService.getPlayerList()).toBe(result);
         expect(Players.find.calls.argsFor(0)).toEqual([{}, {sort: {score: -1, name: 1}}]);
       });
     });
   });
   ```
1. Adjust that test to do something relevant to your application.
1. Run Meteor, visit the app in your browser and check the Velocity status in the top-right corner. If the test is failing, fix it.
1.  Create a file in project root `/tests/cucumber/features/home/view-homepage.feature`:

   ```
   Feature: View homepage

   ...
   ```
1.  Create a file in project root `/tests/cucumber/features/home/step_definitions/view-homepage.js`:

   ```js
   TODO

   ...
   ```
1. Run the Meteor app with Velocity again. Check the status of Velocity and fix any tests.
1. Repeat the steps above until you have enough tests to have some confidence in your code.
