FROM gazebo:latest
# This image extends from nvidia-gazebo image to also provide ROS indigo

USER root

# ----------------------------------------------------------------------------------
# Instructions derived from https://github.com/osrf/docker_images/tree/master/ros/indigo
# ----------------------------------------------------------------------------------
# setup ROS keys
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 421C365BD9FF1F717815A3895523BAEEB01FA116
# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list
# install bootstrap tools
RUN apt-get update && apt-get install --no-install-recommends -y \
    python-rosdep \
    python-rosinstall \
    python-vcstools \
    && rm -rf /var/lib/apt/lists/*

# bootstrap rosdep
RUN rosdep init \
    && rosdep update

# install ros packages
ENV ROS_DISTRO trusty
RUN apt-get update && apt-get install -y \
    ros-indigo-ros-core=1.1.4-0* \
    ros-indigo-ros-base=1.1.4-0* \
	&& apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# setup entrypoint
COPY ./ros_entrypoint.sh /
RUN chmod 755 /ros_entrypoint.sh

USER $USERNAME

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
# ----------------------------------------------------------------------------------
