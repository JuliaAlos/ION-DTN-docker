FROM osrf/ros:jazzy-desktop

# Set non-interactive mode for apt
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y apt-utils && \
    echo "wireshark-common wireshark-common/install-setuid boolean true" | debconf-set-selections && \
    apt-get install -y git build-essential wireshark tshark \
    qtbase5-dev qtchooser qtbase5-dev-tools qt5-qmake && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set the setuid bit on dumpcap
RUN chmod +s /usr/bin/dumpcap

# Create the wireshark group if it doesn't exist and add the user to it
RUN if ! getent group wireshark; then groupadd -g 1001 wireshark; fi && \
    useradd -ms /bin/bash -u 1001 -G wireshark ros2-node

# Define default command.
CMD ["/bin/bash", "-c", "source /opt/ros/jazzy/setup.bash && tail -f /dev/null"]