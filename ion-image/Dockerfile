FROM ubuntu:22.04

# Set non-interactive mode for apt
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apt-utils && \
    echo "wireshark-common wireshark-common/install-setuid boolean true" | debconf-set-selections && \
    apt-get install -y git build-essential autoconf automake libtool wireshark tshark \
    qtbase5-dev qtchooser qtbase5-dev-tools qt5-qmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set the setuid bit on dumpcap
RUN chmod +s /usr/bin/dumpcap

# Create the wireshark group if it doesn't exist and add the user to it
RUN if ! getent group wireshark; then groupadd -g 1001 wireshark; fi && \
    useradd -ms /bin/bash -u 1001 -G wireshark ion-node

# Clone the ION-DTN repository
RUN git clone https://github.com/JuliaAlos/ION-DTN-test.git

# Build and install ION-DTN
WORKDIR /ION-DTN-test

# Create the m4 directory
RUN mkdir -p m4

RUN autoreconf -fi && \
    ./configure && \
    make && \
    make install

# Update the library cache and set the LD_LIBRARY_PATH
RUN echo "/usr/local/lib" >> /etc/ld.so.conf.d/local.conf && \
    ldconfig

# Set the LD_LIBRARY_PATH environment variable
ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

RUN git clone https://github.com/JuliaAlos/ION-DTN-docker.git

RUN \
    mv ION-DTN-docker/test ion-interface/ && \
    rm -rf ION-DTN-docker

# Define default command.
CMD ["tail", "-f", "/dev/null"]
