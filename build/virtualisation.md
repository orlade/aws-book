# Virtualisation

Virtualisation involves creating a computing environment (a "virtual machine" or VM) inside another computing environment. It's kind of like using your computer to simulate another computer, usually with a different operating system.

Virtualisation can get real complicated real fast. The most important thing to understand is that a virtual machine provides a clean slate, which makes your life easier.

In the ideal world, every time you deploy and run your app, it will behave exactly the same way. In reality, the app runs in an environment that is changing all the time. You may install a new program or piece of hardware, update a library or your OS, create a new file or folder, etc. Any of these changes (alone or together) *might* change the behaviour of your app in unpredictable ways that are difficult to trace.

That's where virtualisation comes in. Every time you boot up a new VM, the environment is identical. You may proceed to install programs and change the environment, but you can always start from scratch with a new VM. Thus deploying apps into VMs instead of straight onto the server enables us to guarantee a consistent deployment environment.


## Docker

In recent times, Docker has emerged as the new de facto standard for virtualisation. Built on the Linux container (LXC) technology, Docker containers are like super lightweight VMs that start almost instantly. More importantly (for adoption), Docker provides a user-friendly CLI and GitHub like repository system.

Docker works with the concept of an **image**, like a snapshot of a computing environment (including the OS, file system and installed programs). A `Dockerfile` describes the steps to take a base image and run some commands to set up an application within that environment. The result is saved as a new image.

Once we have a Dockerfile to take a base image and install our application, we can create our own image. This image is stored in a repository (such as the official [Docker Hub][hub]). Then we can run that image on any Linux computer that has Docker installed, and it will run **exactly the same way**. The environment of the host machine doesn't matter (except perhaps for the version of Docker). This is a *big deal* for reliable deployment, so we're going to use it.


## What should I do?

1. Create an account at [Docker Hub][hub].
1. Create a new Automated Build, linked to your source code repository.
1. Create a `Dockerfile` in your project, containing the commands to install your app.
1. Install Docker and test the Dockerfile locally with `docker build -t yourapp .`
1. Commit and push the Dockerfile to Bitbucket, triggering an automated build on Docker hub.
1. Test pulling the remote image and running it locally with `docker run yourname/yourapp`


[hub]: https://hub.docker.com/
