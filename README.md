# pb-robot phoebe

Repository containing Dockerfiles for testing PeopleBot robot phoebe. These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.


## Prerequisites

You need to have Docker in your computer (Docker download: https://www.docker.com/get-docker).
You also need Gazebo7 in your host machine to open simulator GUI (Gazebo download for Ubuntu: http://gazebosim.org/tutorials?tut=install_ubuntu).


## Build docker image and run container 

First you need to build pb:base, then pb:sim_base, then pb:sim_stack and finally pb:sim_latest.
The easiest way to build docker image is to run the following command inside the directory of each Dockerfile. Extensive Docker documentation for building images: https://docs.docker.com/engine/reference/commandline/build/ .

Build docker image from Dockerfile:
```
$ docker build -t Dockerfile .
```

To see repository name, tag name and other information about built images use the following command:
```
$ docker images
```

When running sim_latest or hw_latest container use "master" as name. For tagname use image's repository and tag name (for example pb:sim_latest). Extensive Docker documentation for running containers: https://docs.docker.com/engine/reference/run/ .

Run docker container from built image:
```
$ docker run -it --name [name] [repo:tagname]
```


## Open phoebe model in Gazebo
To use Gazebo you have to build pb:base, pb:sim_base, pb:sim_stack, pb:sim_latest images and run only pb:sim_latest container that you have named "master".

### Note about sourcing catkin workspace:
At the momenent you have to source catkin workspace by yourselt. One way to do it is to write the following command into the every container shell you open:
```
$ source /catkin_ws/devel/setup.bash
```
Another way is to write the following command into the first shell of the container, this way catkin workspace is automatically sourced every time a new shell is launched:
```
$ echo "/catkin_ws/devel/setup.bash" >> ~/.bashrc
```

### Open the model in Gazebo

In the opened container run roscore:
```
$ roscore
```
Then open another shell and in it another bash session of the container:
```
$ docker exec -it master bash
```
In newly opened bash session run the following command:
```
$ rosparam set /use_sim_time true
```
Open world in gazebo. There are many worlds that come with Gazebo installation in /usr/share/gazebo-7/worlds directory in Ubuntu.
```
$ rosrun gazebo_ros gzserver -u --verbose /usr/share/gazebo-7/empty.world  
```
Then open another shell and create a bash session like explained before. In that shell spawn phoebe model into the world:
```
$ rosrun gazebo_ros spawn_model -file `rospack find phoebe_description`/phoebe.urdf -urdf -x 0 -y 0 -z 0 -model phoebe
```
If you want to see the opened world and spawned model in the Gazebo GUI then you have to have Gazebo installed onto your host machine and run following commands in your host machine:
NB! in Ubuntu you may need to add 'sudo' before 'docker'
NB! 'master' is the name of the docker container inside what the gazebo server runs
```
$ export GAZEBO_MASTER_IP=$(docker inspect --format '{{ .NetworkSettings.IPAddress }}' master)
```
```
$ export GAZEBO_MASTER_URI=$GAZEBO_MASTER_IP:11345
```
```
$ gzclient --verbose
```

More information about Gazebo and Docker: https://hub.docker.com/_/gazebo/

### NB! At the moment there are problems with phoebe model and because of that the model might not spawn in gazebo.
