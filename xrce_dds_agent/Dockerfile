FROM ubuntu:jammy

# Example of installing programs
RUN apt-get update \
    && apt-get install -y \
    nano \
    vim \
    git \
    cmake \
    make \
    gcc \
    g++ \
    build-essential \
    && rm -rf /var/lib/apt/lists/*


# Build XRCE agent
RUN git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git 
WORKDIR /Micro-XRCE-DDS-Agent 
RUN mkdir build
WORKDIR /Micro-XRCE-DDS-Agent/build
RUN cmake ..
RUN make 
RUN make install 
RUN ldconfig /usr/local/lib/ 

CMD ["MicroXRCEAgent", "udp4", "-p", "8888"]