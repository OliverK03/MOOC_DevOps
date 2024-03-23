## EXERCISE 1.1

Since we already did "Hello, World!" in the material let's do something else.

Start 3 containers from an image that does not automatically exit (such as nginx) in detached mode.

Stop two of the containers and leave one container running.

Submit the output for docker ps -a which shows 2 stopped containers and one running.

![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/12f68608-4ba9-41d2-8119-9ccda32c26d9)

## EXERCISE 1.2

We have containers and an image that are no longer in use and are taking up space. Running docker ps -a and docker image ls will confirm this.

Clean the Docker daemon by removing all images and containers.

Submit the output for docker ps -a and docker image ls

```shell
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## EXERCISE 1.3

Now that we've warmed up it's time to get inside a container while it's running!

Image devopsdockeruh/simple-web-service:ubuntu will start a container that outputs logs into a file. Go inside the running container and use tail -f ./text.log to follow the logs. Every 10 seconds the clock will send you a "secret message".

Submit the secret message and command(s) given as your answer.
```
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```
## EXERCISE 1.4

For this exercise, I modified the given process starting command to be
```
docker run -it --rm --name website ubuntu bash -c "while true; do echo 'Input website'; read website; echo 'Searching..'; sleep 1; curl http://$website; done"

docker exec -it website bash

apt-get update

apt-get -y install curl
```
After that you can give website input in main terminal and get wanted output for given exercise

## EXERCISE 1.5

Comparing image sizes, we can see that ubuntu image is 5 times more bigger than alpine image

![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/f2b171be-f4af-41f8-bfa8-c3c7b7657892)

Secret message is same on alpine aswell

![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/0fd8cd1f-6d2c-4ffe-b2e6-e6fd2f792411)

