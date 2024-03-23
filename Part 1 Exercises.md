**EXERCISE 1.1**

Since we already did "Hello, World!" in the material let's do something else.

Start 3 containers from an image that does not automatically exit (such as nginx) in detached mode.

Stop two of the containers and leave one container running.

Submit the output for docker ps -a which shows 2 stopped containers and one running.

![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/12f68608-4ba9-41d2-8119-9ccda32c26d9)

**EXERCISE 1.2**

We have containers and an image that are no longer in use and are taking up space. Running docker ps -a and docker image ls will confirm this.

Clean the Docker daemon by removing all images and containers.

Submit the output for docker ps -a and docker image ls

![image](https://github.com/OliverK03/MOOC_DevOps/assets/161088975/90b4ca32-f385-4a07-beb8-f29197c14a9b)
