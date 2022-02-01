# ROS Docker

Credit: https://github.com/gramaziokohler/ros_docker

ROS: ros-noetic-desktop-full

Useful for:
- Running ROS in docker
- Running GUI through VNC in the browser


## SETUP

Build ros image
```
cd ros-noetic-desktop-full/
docker build --rm -f Dockerfile -t ros-noetic-desktop-full .
```

Launch roscore
```
cd ..
docker-compose up -d
```

Run a ros node with mounted dir in catkin_ws/src
```
docker run --name ros_node0 --network ros_default -e DISPLAY=ros_web_gui_1:0.0 -e ROS_MASTER_URI=http://ros-core:11311 -v /Users/zeba/Desktop/Mestrado/robotica/git_reps/smb_common:/root/catkin_ws/src/smb_common -it ros-noetic-desktop-full bash
```
# ALTERAR  PARA SER UM DIRETÓRIO GENÉRICO NO QUAL É SÓ PARA PEGAR E COPIAR OU SYMLINK

Run a ros node without mount
```
docker run --name ros_node1 --network ros_default -e DISPLAY=ros_web_gui_1:0.0 -e ROS_MASTER_URI=http://ros-core:11311 -it ros-noetic-desktop-full bash
```

Access GUI in http://0.0.0.0:8080/vnc.html

Stop:
```
docker-compose stop
```

Check for dependencies:
```
rosdep check --from-paths /root/catkin_ws/src --ignore-src
```
Install dependencies
```
rosdep install -y --from-paths . --ignore-src --rosdistro noetic
```

---
Packages to install:
- python3-catkin-tools # Would have to modify DockerFile to use catkin build