################################################################################
################################################################################
#
#           Stage: base-ros
#
################################################################################
################################################################################


FROM ros:kinetic-perception-xenial as base-ros

# USE German mirror to speed up things
RUN cp /etc/apt/sources.list /etc/apt/sources.list.old \
    && sed -i -e 's/http:\/\/archive\.ubuntu\.com\/ubuntu\// \
    http:\/\/de.archive\.ubuntu\.com\/ubuntu/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        ssh \
        wget \
        zsh \
    && rm -rf /var/lib/apt/lists/*


################################################################################
################################################################################
#
#           Stage: hrs-ros
#
################################################################################
################################################################################

FROM base-ros as hrs-ros

# USE German mirror to speed up things
RUN cp /etc/apt/sources.list /etc/apt/sources.list.old \
    && sed -i -e 's/http:\/\/archive\.ubuntu\.com\/ubuntu\// \
    http:\/\/de.archive\.ubuntu\.com\/ubuntu/' /etc/apt/sources.list

# Install apt dependencies
RUN apt update && \
        apt install -y --no-install-recommends \
        python-catkin-tools \
        python-pip \
        #ros-kinetic-tf2-ros \
        #ros-kinetic-tf \
        #ros-kinetic-fiducial-msgs \
    && rm -rf /var/lib/apt/lists/*

# Install pip dependencies
#RUN pip install --no-cache-dir \
#     numpy==1.23.1 \

    