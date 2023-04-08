## Basic Docker
- Theory About Docker: [#1]
- [#1](../../issues/1)
- [Chao ](https://github.com/NewTechnology123/Docker/issues/1)

- See issue (#1) for more information.
- sjd [Theory Docker] dsdsd
- - sjd [Theory Docker #1] dsdsd
- See issue "Theory Docker #1" for more information.

- New [#1] dsds 
- 2323 (#1)dd
- 2323 [1] 3333
- #Theory-Docker-1 dsdsdsd
- ơ

- [Theory Docker] sdsdsdsds
- [#1]
5. Key Docker Command
- `docker build . `: Build a Dockerfile and create your own Image based on the file
    - `-t NAME:TAG` : Assign a NAME and a TAG to an image
- `docker run IMAGE_NAME` : Create and start a new container based on image IMAGENAME (or use the image id)
    - `--name NAME` : Assign a NAME to the container. The name can be used for stopping and removing etc
    - `-d `: Run the container in detached mode - i.e. output printed by the container is not
    visible, the command prompt / terminal does NOT wait for the container to stop
    - `-it `: Run the container in "interactive" mode - the container / application is then
    prepared to receive input via the command prompt / terminal. You can stop the
    container with` CTRL + C` when using the `-it` flag
    - `--rm `: Automatically remove the container when it's stopped
- `docker ps `: List all running containers
    - `-a `: List all containers - including stopped one
- `docker images `: List all locally stored image
- `docker rm CONTAINER `: Remove a container with name CONTAINER (you can also use the
container id)
- `docker rmi IMAGE` : Remove an image by name / id
- `docker container prune` : Remove all stopped containers
- `docker image prune `: Remove all dangling images (untagged images or unusing)
    - `-a `: Remove all locally stored images
- `docker push IMAGE` : Push an image to DockerHub (or another registry) - the image name/
tag must include the repository name/ url
- `docker pull IMAGE` : Pull (download) an image from DockerHub (or another registry)
## Step build and run
- `docker build .`
- `docker run -p 3000:3000 {containerid} `
