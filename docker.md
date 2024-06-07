# Docker & Docker Compose

## IMAGES
`docker pull image`      # Looks locally for an image, then remotely (DockerHub) and stores it locally (happens automatically with the pull and run commands)

`docker pull <registryName>:<port> -u <userName> -p <password>`     # Pulls from specific registry

`docker image push <images>`                                                                        # Push images to registry

`docker build . -t brooksdra/my-custom-app`       Builds the image and saves it to your local repository and gives it a -t (tag) of brooksdra/my-custom-app

`docker images`                                        # List all active images (use -a for all images, default hides intermediate images)
`docker run image_name`                      #    Run images as container, -it puts you in running container with a bash instance -d runs it disconnected, so you are returned to the current local prompt 
												The -t is runs in terminal mode and -i listens to the standard input, so when you type command they make their way to the docker container you are attached to.
												
`docker image tag <currentTag> <desiredTag>`         # Retag and existing image (makes the desiredTag while keeping the currentTag) both back to the same hash

`docker rmi image_name or id partial`             # Removal all images
`docker rmi $(docker images -aq)`                    # Removal all images

Cleanup most of the system:
`docker system df`                                                # show space used by docker)
`docker system prune`                                       # remove unused data 
                                                                                     -a to remove all unused images, not just dangling ones
                                                                                     --volumes to remove all volumes (careful with this one!) 
`docker system prune -a --volumes`                  # delete images without a container attached and remove all volumes (careful with volumes)

Advanced image manipulation
`docker save <image>:<tag>`                            # Export image to tarBall
`docker load <tarBall>`                                        # Import image from tarBall


## CONTAINERS
`docker execute container_id`        #Execute a command on said container
`docker container ls`                          # List containers
`docker ps`                                          # List all running containers  
`docker ps -a`                                      # List all containers running or otherwise
`docker stop container_id or name`   # Stops the container but does not remove it (it can be started again!)
`docker pause container_id or name`       # Pauses the container
`docker unpause container_id or name`   # Continues the container


`docker run -it daveb/mdb `                 #Runs the container so you can see the sysout in the same window

`docker rm container_id or name`  # Remove containers, they must be stopped (both stopped and running containers stay on the system until they are removed)
`docker rm -f $(docker ps -aq)`        #Removal all containers by id only (-aq), this only works in PowerShell, cmd has trouble with -aq 

`docker inspect container_id`           # Provides detailed description of the current docker container

`docker attach container_name`                # Reattach to an already running container similar to -it, so you are inside the running command
`docker exec -it container_id bash  `          # Use a different session to attach to a running container (use sh if bash not available in said container)
examples:
`docker exec -it container_id mysql -p `      # Connect to a mysql container using the mysql command line tool, you will need the password.
`docker port container_id  `                          # Show mapped ports

### Container Control
Copy a file from host system into a running docker container
docker cp c:\downloads\CilaServicesData.json <container-name-or-id>:/tmp/CilaServicesData.json
docker exec <container-name-or-id>mongoimport -d DataCommons -c sortDataMongo --file /tmp/CilaServicesData.json
Live example with authentication:
docker exec mongodb mongoimport --username engineer --password pro... --authenticationDatabase admin -d DataCommons -c sortDataMongo --file /tmp/CilaServicesData.json

The Tutorial as of 2022-09-19 uses a containerized git image to clone a github project, then a the copy command to get the clone onto the local file system.


## NETWORKING
`docker network create network_name`              Create a new unique docker network              
`docker network ls`                               List current networks
`docker network inspect network_name`             List network details

`docker run -p 80:5000 image_name`				Maps the docker host port 80 to the container port 5000. You can thus run many images as long as they each map to a different host port.
												Note that every container also gets a local ip address on the docker host and a corresponding hostname similar to the container name.

`docker run -p 80:8080 -p 5000:5000 image_name`	Image to map multiple ports 

Network-alias adds a name to the internal DNS for container being launched (mysql example)
`docker run -d --network network_name --network-alias mysql -v todo-mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=todos mysql:5.7`

Docker networking...
Bridge default there is a gateway 172.17.0.1 and each container gets a private ip 172.17.0.* to that gateway and must be mapped to the docker host 
       or accessed with the 172 ip from withing the docker host
None (`docker run ubuntu --network=none`) the containers are not on any network at all, no mappings 
Host (`docker run ubuntu --network=host`) maps internal port to docker host ports similar to -p 5000:5000.  
     Note you cannot run multiple containers on the same host as the ports will conflict

### Network tool
`docker run -it --network network_name nicolaka/netshoot`
This drops you in the netshoot terminal
dig mysql 
This should provide some information


## VOLUME MAPPING
When a container is created, all of the data and volumes are by default mapped inside the container and will last only as long as the container itself. !!!  
For data to persist past the container, map a docker host file path to a container path using the -v parameter

Named Volumes are great if we simply want to store data and we don't have to worry about where the data is stored.
`docker volume create volume_name`
`docker volume ls`
`docker volume inspect volume_name`
`docker volume prune`                                   # remove all unused volumes
`docker volume rm volume_name. `            # remove specified volume

Bind Mounts control the exact mountpoint on the host. 
Maps the /var/lib/mysql directory inside the container to the docker host directory /c/ProgramData/DockerData/mariadb

`docker run --name maria-db -e MYSQL_ROOT_PASSWORD='proexectedyne' -d -p 3306:3306 -v /c/ProgramData/DockerData/mariadb:/var/lib/mysql mariadb:10.3.12`

# Docker Compose
docker-compose.yml is the default file that lists a grouping of services provided within a deployment

`docker-compose up -d`                        # starts up the compose files components (-d to run everything in the background with minimal screen output)
`docker-compose stop`                        # stops the containers
`docker-compose start`                        # starts the containers
`docker-compose down`                         # stop the containers

`Docker-compose pull`                          # pull all images referenced in the file

`docker-compose logs -f`                      # Shows a tail log from every container running in this compose instance in temporal order
`docker-compose logs -f container_name`       # Include container_name to filter log output

Docker Compose has a way to override files: See https://docs.docker.com/compose/extends/ 
for an example of two default named files as docker-compose.yml and docker-compose.override.yml

There is also a similar feature for running administrative tasks (docker-compose.admin.yml) like building a database 

This can also be accomplished by specifically listing the files
`docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d`


## Interesting Docker Desktop tutorial which sheds some light on things:
if MacOS Tutorial run `chsh –s /bin/zsh` to make zshell the default shell... 

I think this is only for this tutorial:
if MacOS chsh –s /bin/zsh
This runs the alpine/git image and clones a git repo
docker run --name repo alpine/git clone https://github.com/docker/getting-started.git
This then copies that repo to your local pc direcytory the . Can be anywhere on the pc
`docker cp repo:/git/getting-started/ .`
cd getting-start
This builds the local files into a docker101tutorial image
docker build -t docker101tutorial .

This runs the tutorial application on port 80 with the container named docker-tutorial
`docker run -d -p 80:80 --name docker-tutorial docker101 tutorial`
- Application is running on localhost of port 80
- Application is available on the network using http://172.16.100.144:80 which changed to http://172.16.100.144/tutorial  

This runs the tutorial application on port 8088 with the container named docker-tutorial2, just for funzies
`docker run -d -p 8088:80 --name docker-tutorial2 docker101 tutorial`

`docker tag docker101tutorial davebpro.../docker101tutorial`
`docker push davebpro.../docker101tutorial`

Also run the following for funzies:
`docker run -d -p 81:80 --name get-started docker/getting-started`
Modified from Tutorial of the first app
`docker run -d -p 80:80 docker/getting-started`
