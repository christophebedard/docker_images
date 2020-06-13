FROM osrf/ros2:devel

RUN apt-get update && apt-get install -q -y \
    openssh-client \
    htop \
    vim \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install -U \
    colcon-coveragepy-result

# After apt install sudo
RUN echo 'ALL ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Temporary fix: https://github.com/sudo-project/sudo/issues/42#issuecomment-609079906
RUN echo "Set disable_coredump false" >> /etc/sudo.conf

COPY env.sh /etc/profile.d/ade_env.sh
COPY entrypoint /ade_entrypoint
ENTRYPOINT ["/ade_entrypoint"]
CMD ["/bin/sh", "-c", "trap 'exit 147' TERM; tail -f /dev/null & while wait ${!}; [ $? -ge 128 ]; do true; done"]
