FROM osrf/ros2:devel

RUN apt-get update && apt-get install -q -y \
    openssh-client \
    wget \
    htop \
    vim \
    silversearcher-ag \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -q -y \
    libasio-dev \
    libtinyxml2-dev \
    lcov \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install -U \
    colcon-lcov-result \
    colcon-coveragepy-result \
    coverage

RUN apt-get update && apt-get install -q -y \
    lttng-tools \
    liblttng-ust-dev \
    python3-lttng \
    python3-babeltrace \
    python3-pandas

RUN mkdir /root/ws
COPY . /root/ws
WORKDIR /root/ws

RUN wget https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos \
    && mkdir src \
    && vcs import src < ros2.repos

# install dependencies
RUN apt-get update && rosdep install -y \
    --from-paths src \
    --ignore-src \
    --skip-keys "console_bridge fastcdr fastrtps rti-connext-dds-5.3.1 urdfdom_headers" \
    && rm -rf /var/lib/apt/lists/*

# After apt install sudo
RUN echo 'ALL ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Temporary fix: https://github.com/sudo-project/sudo/issues/42#issuecomment-609079906
RUN echo "Set disable_coredump false" >> /etc/sudo.conf

COPY env.sh /etc/profile.d/ade_env.sh
COPY entrypoint /ade_entrypoint
ENTRYPOINT ["/ade_entrypoint"]
CMD ["/bin/sh", "-c", "trap 'exit 147' TERM; tail -f /dev/null & while wait ${!}; [ $? -ge 128 ]; do true; done"]
