# DOCKER

## Commands Docker Hub

| Docker Syntax                | Description                                                                    |
| ---------------------------- | -------------------------------------------------------------------------------|
| docker login [repo]:[port]   | Authenticate to Docker Hub (or other Docker registry).                         |
| docker logout [repo]:[port]  | Authenticate to Docker Hub (or other Docker registry).                         |

## Working With Containers

| Docker Syntax                                 | Description                                                                                          |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| docker ps                                     | List all running containers.                                                                         |
| docker ps -a                                  | List all container instances, with their ID and status.                                              |
| docker exec [container name or ID] [shell]    | Executes a command within a running container.                                                       |
| docker run -it []                             | Runs an image, creating a container and changing the terminal to the terminal within the container.  |
| docker run -p $HOSTPORT:$CONTAINERPORT -d []  | Run an image in detached mode with port forwarding.                                                  |
| ctrl+p then ctrl+q                            | From within the container’s command prompt, detach and return to the host’s prompt.                  |
| docker attach [container name or ID]          | Changes the command prompt from the host to a running container.                                     |
| docker start [container name or ID]           | Start a container.                                                                                   |
| docker stop [container name or ID]            | Stop a running container through SIGTERM.                                                            |
| docker kill [container name or ID]            | Stop a running container through SIGKILL.                                                            |
| docker logs [container name or ID]            | Displays the logs from a running container.                                                          |
| docker logs --tail 100 [container name or ID] | Print the last 100 lines of a container’s logs.                                                      |
| docker port []                                | Displays the exposed port of a running container.                                                    |
| docker diff []                                | Lists the changes made to a container.                                                               |
| docker rm [container name or ID]              | Delete a stopped container.                                                                          |
| docker rm -f [container name or ID]           | Force stop and delete a container.                                                                   |
| docker rm -f $(docker ps -aq)                 | Delete all running and stopped containers                                                            |
| docker rm $(docker ps -q -f “status=exited”)  | Delete all stopped containers                                                                        |

## Working with Images

| Docker Syntax                                 | Description                                                                                          |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| docker images                                 | Lists all images on the local machine.                                                               |
| docker history [image]                        | Lists the history of an image.                                                                       |
| docker search [image]:[tag]                   | Search Docker Hub for images.                                                                        |
| docker pull [image]:[tag]                     | Downloads an image from Docker Hub.                                                                  |
| docker push [image]:[tag]                     | Uploads an image to Docker Hub. You must be authenticated to run this command.                       |
| docker commit [image]                         | Save a container as an image.                                                                        |
| docker save [image] -o [filename].tar         | Save an image to a tar archive.                                                                      |
| docker load -i [filename].tar                 | Loads an image from file.                                                                            |
| docker rmi [image]:[tag]                      | Delete an image from the local image store                                                           |
| docker tag [image]:[tag] [newimage]:[newtag]  | Retag a local image with a new image name and tag                                                    |
| docker tag [image]:[tag] [image]:[newtag]     | Retag a local image with a new tag                                                                   |
| docker build -t [image]:[tag] .               | Build an image from the Dockerfile in the current directory and tag the image.                       |

## Working with docker networks

| Docker Syntax               | Description                                     |
| --------------------------- | ----------------------------------------------- |
| docker network ls           | List all the networks created.                  |
| docker network create       | Create a new network with the specified name.   |
| docker network connect      | Connect a container to a network.               |
| docker network disconnect   | Disconnect a container from a network.          |
| docker network inspect      | Display detail information for a network.       |
| docker network rm           | Delete network.                                 |
