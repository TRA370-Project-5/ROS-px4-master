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
COPY PX4-Autopilot /PX4-Autopilot
RUN bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
WORKDIR PX4-Autopilot
RUN make px4_sitl

ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

#ENV PX4_GZ_STANDALONE=1

CMD ["make", "px4_sitl", "gz_x500_depth"]

# https://discuss.px4.io/t/solved-custom-quad-gazebo-model-runs-with-slow-real-time-factor/15784

# PILLA TOOLS/Simulation/gz/worlds/....
# Här bygger man även nya modeller