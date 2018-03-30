FROM ubuntu:xenial
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list' && \
    sh -c 'apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116' && \
    apt-get update && \
    apt-get install -y ros-lunar-desktop-full wget vim git && \
    rosdep init && \
    rosdep update && \
    mkdir -p /catkin_ws/src && \
    /bin/bash -c 'echo "source /opt/ros/lunar/setup.bash" >> /.bashrc && source /.bashrc && cd /catkin_ws && catkin_make' && \
    /bin/bash -c 'echo "source /catkin_ws/devel/setup.bash" >> /root/.bashrc && source /root/.bashrc'
