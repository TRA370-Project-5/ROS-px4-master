FROM osrf/ros:humble-desktop-full


# Example of installing programs
RUN apt-get update \
    && apt-get install -y \
    build-essential \
    curl \
    git \
    libclang-dev \
    nano \
    python3-pip \
    vim \
    && rm -rf /var/lib/apt/lists/*

# Install ROS stuff
RUN apt-get update \
    && apt-get install -y \
    ros-humble-ros-ign-bridge \
    ros-humble-action-msgs \
    ros-$ROS_DISTRO-foxglove-bridge \
    && rm -rf /var/lib/apt/lists/*


# Install Rust and the cargo-ament-build plugin
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain 1.74.0 -y
ENV PATH=/root/.cargo/bin:$PATH
RUN cargo install cargo-ament-build

RUN pip install --upgrade pytest 

# Install the colcon-cargo and colcon-ros-cargo plugins
RUN pip install git+https://github.com/colcon/colcon-cargo.git git+https://github.com/colcon/colcon-ros-cargo.git

# Example of copying a file
#COPY config/ /site_config/


# Create a non-root user
ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && mkdir /home/$USERNAME/.config && chown $USER_UID:$USER_GID /home/$USERNAME/.config


# Set up sudo
RUN apt-get update \
  && apt-get install -y sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  && rm -rf /var/lib/apt/lists/*


# Copy the entrypoint and bashrc scripts so we have 
# our container's environment set up correctly
COPY entrypoint.sh /entrypoint.sh
COPY bashrc /home/${USERNAME}/.bashrc


# Set up entrypoint and default command
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
CMD ["bash"]