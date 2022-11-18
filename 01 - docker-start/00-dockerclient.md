# Getting Familiar with the Docker Client

To check that everything is set-up, run the following:

```console
 docker run hello-world
```
If it is first time we have run this command, terminal will return such output.

```console
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest: sha256:faa03e786c97f07ef34423fccceeec2398ec8a5759259f94d99078f264e9d7af
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```


## Pulling an Image

Now that everything is set up, let's walk through how to run your first container. We will run an ubuntu container, and get familiar with some of the =docker= commands.

In your terminal, run the following:

```console
 docker pull ubuntu
```

If you get a permission denied error, it may require you to run =sudo docker pull=. To avoid this in the future, try:

#+BEGIN_EXAMPLE
 sudo usermod -aG docker $USER
#+END_EXAMPLE

Then exit and restart your terminal.

The pull command fetches the latest ubuntu image from [Dockerhub](https://hub.docker.com/), a public container registry. To see which images are downloaded to your machine, run the following:

```console
docker images
```
For my case, output looks like this 
```console
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
ubuntu        latest    a8780b506fa4   2 weeks ago     77.8MB
hello-world   latest    feb5d9fea6a5   14 months ago   13.3kB
```

Now that we have pulled our first image, it is time to run the container.

## Running a Container
In your terminal, run the following:
```console
 docker run ubuntu echo "hello!"
```

What just happened?

1. When you call =run=, the Docker client calls the Docker daemon
2. The Docker daemon checks locally to see if the image is available, if it is not, it downloads it from Dockerhub 
3. If the image is present, the daemon creates the container and runs the command you specified in the containter
4. The output of the command is streamed to the client and you observe it

In our above example, the Docker client ran the command in the container and then exited out...in a matter of seconds! The speed with which containers can be created and commands run makes them very useful in many use cases. 

Note that the container exits after the command you pass to it is run. For it to not exit, you will need to run the container in *interactive* mode:
```console
 docker run -it ubuntu 
```

This drops you in to the container. Try out your favourite commands (=ls -la=).
this is an output for my case...
```console
root@b917744064ee:/#
```
You can exit the container by typing =exit=.
```console
root@b917744064ee:/# exit
exit

C:\Users\johnDoe>
```

If you want to see what containers you have running, type:
```console
 docker ps
```
Output for my case
```console
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

Since you have exited out of all the containers, you will see nothing here. To see the containers that you have run, try:
```console
 docker ps -a
```

This shows you a list of all the containers, you have run and also their Status. To get just the container IDs, you can use =docker ps -a -q=. The point to note here is that the image persists but the containers only exist for the time that you want to run them. You essentially have many machines with various configurations running on your machine or server as you need them. 
```console
CONTAINER ID   IMAGE         COMMAND                CREATED             STATUS                         PORTS     NAMES
b917744064ee   ubuntu        "bash"                 8 minutes ago       Exited (0) 7 minutes ago                 magical_chatterjee
a331508c9378   ubuntu        "echo 'hello world'"   10 minutes ago      Exited (0) 10 minutes ago                confident_chandrasekhar
d70e61f6a819   hello-world   "/hello"               About an hour ago   Exited (0) About an hour ago             admiring_cori
```
If at any time, you want to clean up images and containers, you can use:
```console
 docker rm $(docker ps -a -q)
```

This clears all the containers on your machine. Similarly, to remove all images, use =docker rmi $(docker images -a -q)=.
