FROM ubuntu:jammy

# Example of installing programs
RUN apt-get update \
    && apt-get install -y \
    nano \
    sudo \
    vim \
    git \
    cmake \
    make \
    gcc \
    g++ \
    build-essential \
    lsb-release \
    wget \
    && rm -rf /var/lib/apt/lists/*


# Build PX4 tools
RUN git clone https://github.com/PX4/PX4-Autopilot.git --recursive px4
RUN bash ./px4/Tools/setup/ubuntu.sh
WORKDIR px4
RUN make px4_sitl

CMD ["make", "px4_sitl_default", "none_iris"]