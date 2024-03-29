# DevOps With Docker Course exercises

## Exercise 1.1

Since we already did "Hello, World!" in the material let's do something else. Start 3 containers from an image that does not automatically exit (such as nginx) in detached mode.Stop two of the containers and leave one container running.

Submit the output for docker ps -a which shows 2 stopped containers and one running.

&nbsp;

**Output**
![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/c09ae3e5-512f-4fe8-a743-4510bd911fb2)

&nbsp;

## Exercise 1.2

We have containers and an image that are no longer in use and are taking up space. Running docker ps -a and docker image ls will confirm this. Clean the Docker daemon by removing all images and containers.

Submit the output for docker ps -a and docker image ls

&nbsp;
**Containers:**
```
  CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
**Images:**
```
  REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

&nbsp;

## Exercise 1.3

Now that we've warmed up it's time to get inside a container while it's running!

Image devopsdockeruh/simple-web-service:ubuntu will start a container that outputs logs into a file. Go inside the running container and use tail -f ./text.log to follow the logs. Every 10 seconds the clock will send you a "secret message".

Submit the secret message and command(s) given as your answer.

&nbsp;

**Output**
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```
&nbsp;

## Exercise 1.4

Start a Ubuntu image with the process
```
sh -c "while true; do echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://$website; done"
```
You will notice that a few things required for proper execution are missing. Be sure to remind yourself which flags to use so that the container actually waits for input.

Note also that curl is NOT installed in the container yet. You will have to install it from inside of the container.

Test inputting helsinki.fi into the application. It should respond with something like

```
<html>
  <head>
    <title>301 Moved Permanently</title>
  </head>

  <body>
    <h1>Moved Permanently</h1>
    <p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
  </body>
</html>
```
This time return the command you used to start process and the command(s) you used to fix the ensuing problems.

**Shell**
```
docker run -d -it --name website ubuntu sh -c "echo 'Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
docker exec -it website bash
apt-get update
apt-get -y install curl
helsinki.fi
```

## Exercise 1.5
Here is the same application but instead of Ubuntu is using Alpine Linux:
```
devopsdockeruh/simple-web-service:alpine
```
Pull both images and compare the image sizes. Go inside the Alpine container and make sure the secret message functionality is the same. Alpine version doesn't have ```bash``` but it has ```sh```, a more bare-bones shell.

**Shell**
```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
ubuntu       latest    ca2b0f26964c   4 weeks ago    77.9MB
alpine       latest    05455a08881e   2 months ago   7.38MB
```

**Output**
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

## Exercise 1.6
Run ```docker run -it devopsdockeruh/pull_exercise.```

The command will wait for your input.
Navigate through the Docker hub to find the docs and Dockerfile that was used to create the image.
Read the Dockerfile and/or docs to learn what input will get the application to answer a "secret message".
Submit the secret message and command(s) given to get it as your answer.

**Shell**

```
run -it devopsdockeruh/pull_exercise.
```
**Output**

```
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## Exercise 1.7
We can improve our previous solutions now that we know how to create and build a Dockerfile.

Create a new file ```script.sh``` on your local machine with the following contents:

```
while true
do
  echo "Input website:"
  read website; echo "Searching.."
  sleep 1; curl http://$website
done
```

Create a Dockerfile for a new image that starts from _ubuntu:22.04_ and add instructions to install ```curl``` into that image. Then add instructions to copy the script file into that image and finally set it to run on container start using CMD.

After you have filled the Dockerfile, build the image with the name "curler".

The following should now work:
```
docker run -it curler

  Input website:
  helsinki.fi
  Searching..
  <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
  <html><head>
  <title>301 Moved Permanently</title>
  </head><body>
  <h1>Moved Permanently</h1>
  <p>The document has moved <a href="https://www.helsinki.fi/">here</a>.</p>
  </body></html>
```

**Dockerfile**
```
# Start from Ubuntu 22.04 image
FROM ubuntu:22.04

# Install curl
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*

# Copy the script file into the image
COPY script.sh /usr/src/app/

# Set permissions to run the script
RUN chmod +x /usr/src/app/script.sh

# Set working directory
WORKDIR /usr/src/app

# Set the script to run on container start using CMD
CMD ./script.sh
```

## Exercise 1.8

By default our ```devopsdockeruh/simple-web-service:alpine``` doesn't have a CMD. Instead, it uses ENTRYPOINT to declare which application is run.

In this exercise create a Dockerfile and use FROM and CMD to create a brand new image that automatically runs ```server```.

The Docker documentation CMD says a bit indirectly that if a image has ENTRYPOINT defined, CMD is used to define it the default arguments.

Tag the new image as "web-server"

Return the Dockerfile and the command you used to run the container.

**Dockerfile**
```
FROM devopsdockeruh/simple-web-service:alpine

CMD server
```
**Shell**
```
docker run -it web-server
[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:   export GIN_MODE=release
 - using code:  gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /*path                    --> server.Start.func1 (3 handlers)
[GIN-debug] Listening and serving HTTP on :8080
```











