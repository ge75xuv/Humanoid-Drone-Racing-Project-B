################################################################################
################################################################################
#
#           Stage: base-ros
#
################################################################################
################################################################################


FROM osrf/ros:kinetic-desktop-full as base-ros

# USE German mirror to speed up things
RUN cp /etc/apt/sources.list /etc/apt/sources.list.old \
    && sed -i -e 's/http:\/\/archive\.ubuntu\.com\/ubuntu\// \
    http:\/\/de.archive\.ubuntu\.com\/ubuntu/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        ssh \
        wget \
        zsh \
        python-catkin-tools \
        python-pip \
    && rm -rf /var/lib/apt/lists/*


################################################################################
################################################################################
#
#           Stage: hrs-ros
#
################################################################################
################################################################################

FROM base-ros as hrs-ros

# Install apt dependencies
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_FRONTEND teletype
RUN apt update && \
        yes | apt install -y --no-install-recommends \
        'ros-kinetic-nao*' \
    && rm -rf /var/lib/apt/lists/*

# Copy PyNaoQi into image and add to pythonpath
ADD pynaoqi /pynaoqi
ENV PYTHONPATH "${PYTHONPATH}:/pynaoqi"
ENV LD_LIBRARY_PATH "${LD_LIBRARY_PATH}:/pynaoqi"


################################################################################
################################################################################
#
#           Stage: base-ros-user
#
################################################################################
################################################################################

FROM hrs-ros as hrs-ros-user

ARG USERNAME=devel
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    #
    # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# ********************************************************
# * Anything else you want to do like clean up goes here *
# ********************************************************

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME
#ADD .bashrc /home/$USERNAME/.bashrc
################################################################################
################################################################################
#
#           Stage: team-ros
#
################################################################################
################################################################################

FROM hrs-ros-user as team-ros

# set team-specific settings in separate layer to speed up builds
ENV NAO_IP "10.152.246.123"
# add ros to .bashrc so that its sourced in each terminal
RUN echo "source /opt/ros/kinetic/setup.bash" >> /home/$USERNAME/.bashrc

    