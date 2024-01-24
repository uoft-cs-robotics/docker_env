ARG image=osrf/ros:noetic-desktop-full
FROM ${image}

ARG DEBIAN_FRONTEND=noninteractive
# ARG workstation_ip=192.168.0.1
# ARG use_robotiq=0
# ARG build_dope=1
# ARG build_contactgraspnet=1
# ARG build_megapose=1
ENV WS_DIR="/root/git"
WORKDIR ${WS_DIR}

SHELL ["/bin/bash", "-c"]
# Dependencies for latency plot
RUN apt-get update && apt-get -y  upgrade && apt-get install -y \
    curl \
    grep \
    build-essential \
    make \
    libnuma-dev \
    python3 \
    python3-distutils \
    gnuplot-qt \ 
    sshpass \
    iproute2 \
    python3-pip \
    gnome-terminal\
    nano\
    vim \
    git \ 
    sudo 

# Dependencies for Bash unit-tests
RUN apt-get update && apt-get install -y \
    bats \
    dialog \
    tmux \
    iputils-ping 	

RUN apt-get update && apt-get -y  upgrade
RUN echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
RUN apt-get install -y ros-noetic-gazebo-ros \
                    ros-noetic-control-toolbox \
                    ros-noetic-realtime-tools \
                    ros-noetic-ros-control \
                    ros-noetic-ros-controllers \
                    ros-noetic-gazebo-ros-control
#                     ros-noetic-joystick-drivers \

ARG DEBIAN_FRONTEND=dialog                    
