# Description 
dockerfile and docker compose yaml files used to build docker environments 

## Dependancies
- docker.io
- docker compose 

## Build instructions 
```
cd ~
git clone https://github.com/uoft-cs-robotics/docker_env
```

```
cd ~/docker_env 
docker compose -f csc477/docker-compose-gui.yml build
docker compose -f csc477/docker-compose-gui.yml create
```
## Note to CSC477 students 
This docker setup is useful when you're using your own or DH Labs Ubuntu machine or if you are accessing UTM lab machines using VNC. This setup is not tested for Windows/Mac host machines. 


## Usage 

Start the prebuilt container 
```
cd ~/docker_env 
docker compose -f csc477/docker-compose-gui.yml start
```

To get GUI access run this in every terminal you are running the docker container's terminal. or you can add it to your ~/.bashrc
```
xhost +local:docker
```

To open docker container's terminal 
```
docker exec -it csc477 bash 
```

The home folder in this repo will be mounted to the docker container at /root/home inside the docker container (see file [docker-compose.yml](csc477/docker-compose.yml) line 23). This happens when you run "docker-compose ... create". You can create your ROS workspace here and compile it from within the docker container and <b>read its source code from the host machine using your favorite IDE</b>. You might also have to run the following from inside the docker to access the directories and files inside home, 
```
chmod 777 -R /root/home
```

## Build instructions for CSC477 ROS packages 

Assuming you already have the docker container running,open a new terminal inside the docker running by running this in the hostmachine's terminal 
```
docker exec -it csc477 bash 
```
Once you have opened a bash terminal inside your container, create your catkin workspace, 

```
cd /root/home 
mkdir csc477_ws/src -p 
cd csc477_ws/src 
catkin_init_workspace
```

Clone the ROS packages to the new workspace, 
```
cd /root/home/csc477_ws/src 
git clone https://github.com/florianshkurti/csc477_winter24
cd /root/home/csc477_ws 
catkin_make
```

Make sure you add either run 
```
source /root/home/csc477_ws/devel/setup.bash 
```
in every terminal you want to run nodes/launch files from this workspace or add it to ~/.bashrc by running the below in the docker container's terminal

```
echo "source /root/home/csc477_ws/devel/setup.bash" >> ~/.bashrc
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
