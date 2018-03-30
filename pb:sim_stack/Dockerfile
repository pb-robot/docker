FROM pb:sim_base
RUN cd /catkin_ws/src && \
    # 1500 controller ja dynamixel lisatud sest: errors/1500controller (pic)
    git clone https://github.com/pb-robot/cyton_gamma_1500_controller.git && \
    git clone https://github.com/arebgun/dynamixel_motor.git && \
    git clone https://github.com/pb-robot/cyton_gamma_1500_description.git && \
    git clone https://github.com/pb-robot/cyton_gamma_1500_minicam_description.git && \
    git clone https://github.com/pb-robot/phoebe_description.git && \
    git clone https://github.com/pb-robot/dp_ptu_46_description.git && \
    git clone https://github.com/pb-robot/phoebe.git && \
    git clone https://github.com/ros-drivers/urg_node.git && \
    git clone https://github.com/ros-perception/laser_proc.git && \
    git clone https://github.com/ros-drivers/urg_c.git && \
    apt-get install -y ros-lunar-moveit && \
    /bin/bash -c 'source /root/.bashrc && cd /catkin_ws && catkin_make -DCMAKE_CXX_FLAGS="-std=c++11"'
