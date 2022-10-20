# Working-with-Docker

## Running a one-off container

Docker containers run as long as the process inside the container keeps running. When the process finishes, the container exits.
You can run a simple container to run a single Linux command:

### Pull Smtp4Dev image from Docker Hub
```
docker pull rnwood/smtp4dev
```
## Running an interactive container

One-off containers run and then stop. You can run a long-running process in a container instead, and connect your terminal to the container's terminal.

This is like connecting to a remote machine - any commands you run actually run inside the container:
```
docker run -it alpine
```
The -it flag means runs interactively, with the local terminal attached, and the default command for the Alpine container is to run the Linux shell
Now you're connected to the container, you can explore the environment:
```
ls /
whoami
hostname
cat /etc/os-release

exit
```

### Run Smtp4Dev container locally
```
docker run --rm -it -p 3000:80 -p 2525:25 rnwood/smtp4dev
```
### Try another one
```
docker run -it --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/samples:aspnetapp
```

## Running a background container

Interactive containers are great for testing commands and exploring the container setup, but mostly you'll want to run detached containers.
These run in the background, so the container keeps running until the application process exits, or you stop the container.

You'll use background containers for web servers, batch processes, databases message queues and any other server process.
```
docker run -d -P --name nginx1 nginx:alpine
```
-d flag runs a detached background container

-p publishes network ports so you can send traffic into the container

--name gives the container a name so you can work with it in other commands

## Running custom containers on a Single Machine

### Create a new .Net Core Web API
```
dotnet new webapi -o HelloCode.API --no-https
```

### Test run the web api
```
Run the web api using the Run and Debug section of VS Code or using "dotnet run" command
```

### Add Docker support
```
* Add a Dockerfile using the command palette of VS Code (CMD+SHFT+P)
* Run HelloCode.API using command palette or using the "docker run" command
* Inspect the container image and container using Docker Extention and Docker Desktop
```

## Working with container registries

### Retag and push to Docker Hub:
```
docker login <username>
Password: <password>
docker images
docker tag <source image> <username>/<target image>:<tag>
docker push <username>/<target image>:<tag>
```

### Retag and push to ACR:
```
docker login tshapelabacr01.azurecr.io
Username: tshapelabacr01
Password: zd+sexKFPEK5g9DHcGPzIctuwLJ39Iej
docker images
docker tag <source image> tshapelabacr01.azurecr.io/<target image>:<tag>
docker push tshapelabacr01.azurecr.io/<target image>:<tag>
```

## Lab

We've run containers using public and custom images. All public packages available on [Docker Hub](https://hub.docker.com).

In this lab you'll work with Java containers:

- find a package on Docker Hub which you can use to run a Java app
- run a Java container and confirm which version of Java is installed using the `java -version` command
- now find a *small* image for Java 8, with just the JRE runtime installed

> Stuck? Try [hints](hints.md) or check the [solution](solution.md).

___
## Cleanup

Cleanup by removing all containers:

```
docker rm -f $(docker ps -aq)
```
