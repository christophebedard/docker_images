FROM osrf/ros2:devel

RUN pip3 install -U \
    colcon-coveragepy-result

CMD ["/bin/sh", "-c", "trap 'exit 147' TERM; tail -f /dev/null & while wait ${!}; [ $? -ge 128 ]; do true; done"]
