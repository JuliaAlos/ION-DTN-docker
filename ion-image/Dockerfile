FROM ubuntu:22.04  
 
RUN apt-get update && \
    apt-get install -y git build-essential autoconf automake libtool && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone the ION-DTN repository
RUN git clone https://github.com/nasa-jpl/ION-DTN.git

# Copy the cloned repository into the image
# COPY ../../ION-DTN /ION-DTN

# Build and install ION-DTN
WORKDIR /ION-DTN
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
