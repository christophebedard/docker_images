FROM alpine:latest

RUN apk update && apk add --no-cache bash
RUN apk update && apk add --no-cache git --repository=http://dl-cdn.alpinelinux.org/alpine/edge/main
RUN apk update && apk add --no-cache --virtual .build-deps g++ libffi-dev openssl-dev && \
    apk add --no-cache --update python3 python3-dev && \
    python3 -m ensurepip && \
    pip3 install --upgrade pip setuptools
    # if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    # if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \

RUN apk update && apk add --no-cache mercurial subversion

# After apt install sudo
# RUN echo 'ALL ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

COPY env.sh /etc/profile.d/ade_env.sh
COPY entrypoint /ade_entrypoint
ENTRYPOINT ["/ade_entrypoint"]
CMD ["/bin/sh", "-c", "trap 'exit 147' TERM; tail -f /dev/null & while wait ${!}; [ $? -ge 128 ]; do true; done"]
