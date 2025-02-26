
# Getting Familiar with a Dockerfile

## Terminology Review
- Image: Blueprint for the container you want to build. Often based on other images.
- Layer: Modification to a base image. Layers are supplied in sequence to create a final image.
- Container: Built from an image. Can have many copies of the same image running as containers.
- Dockerfile: Instructions for how to build an image. Has a special syntax that contains all the commands that are routed to the command line to build an image. 
- Commit: One of the benefits of Docker is that it offers version control of a computing environment. This is handled similar to git.
- DockerHub/Container Registry: A repository for Docker containers. Can have public and private. Dockerhub (public) vs Azure/AWS offerings of container registries (private).

## Dockerfile Example
A Dockerfile has INSTRUCTIONS and arguments. It is not neccessary that they be capitalized, but it is the convention.

### FROM

The *FROM* statement specifies the base image. In our example, we are taking the =postgres= base image from [Dockerhub](https://hub.docker.com/_/postgres/). 

### LABEL

The *LABEL* statement adds metadata to the image. It is optional, but is helpful if you are pushing your containers to a shared registry so people know who to contact in case of an issue.

### RUN

The *RUN* statement is the workhorse of the Dockerfile. In our case, we are using it to run shell commands. These commands have nothing to do with Docker but are basic Linux commands. 

### WORKDIR

The *WORKDIR* statement is often sued to specify a working directory. Any subsequent commands will assume that is the working directory.

### ADD

The *ADD* statement lets you copy files from the host machine to the docker container. 

### CMD

The *CMD* statement is used to provide defaults when executing a container. Only one *CMD* statement is valid per container, and if you provide several, only the last one will be used by the container. 

More information on Docker commands can be found here: https://docs.docker.com/engine/reference/builder/




