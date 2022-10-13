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


### Running a background container

Interactive containers are great for testing commands and exploring the container setup, but mostly you'll want to run detached containers.
These run in the background, so the container keeps running until the application process exits, or you stop the container.

You'll use background containers for web servers, batch processes, databases message queues and any other server process.
```
docker run -d -P --name nginx1 nginx:alpine
```
-d flag runs a detached background container

-p publishes network ports so you can send traffic into the container

--name gives the container a name so you can work with it in other commands
