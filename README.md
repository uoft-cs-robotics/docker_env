# Description 
dockerfile and docker compose yaml files used to build docker environments 

## Dependancies
- docker.io
- docker compose 

## Build instructions 


```
cd <path_to_repository>/docker_env 
docker-compose -f csc477/docker-compose-gui.yml build
docker-compose -f csc477/docker-compose-gui.yml create
```
## Note to CSC477 students 
This docker setup is useful when you're using your own Ubuntu machine or if you are accessing UTM lab machines using VNC. This setup is not tested for Windows/Mac host machines. 


## Usage 

Start the prebuilt container 
```
cd <path_to_repository>/docker_env 
docker-compose -f csc477/docker-compose-gui.yml build
```

To get GUI access run this in every terminal you are running the docker container's terminal. or you can add it to your ~/.bashrc
```
xhost +local:docker
```

To open docker container's terminal 
```
docker exec -it csc477 bash 
```

The home folder in this repo will be mounted to the docker container at /root/home inside the docker container (see file [docker-compose.yml](csc477/docker-compose.yml) line 23). This happens when you run "docker-compose ... create". You can create your ROS workspace here and compile it from within the docker container and yet read its source code from the host machine using your favorite IDE. You might also have to run the following from inside the docker to access the directories and files inside home, 
```
chmod 777 -R /root/home
```

## Notes: 
- If you are unable to access a directory or file in the host machine you created inside the docker container, run from inside the docker container,
```
chmod 777 <filename>
chmod 777 -R <directory name>
```
- Depending on your version of docker compose you either to run "docker-compose ..." or "docker compose ..."
- Make sure you have added your user to docker group inorder to run docker commands without sudo 
- VSCode is not installed inside the docker. see usage instructions on how to view and edit code stored in the docker container
