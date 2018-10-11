# Run kmymoney in a container
#
# docker run -it \
#       -v /tmp/.X11-unix:/tmp/.X11-unix \ # mount X11 for display
#       -e DISPLAY=unix$DISPLAY \
#       -v $HOME/kmymoney_state:/home/kmymoney \  # if you want to save state
#       --device /dev/snd \ # if you want sound
#       --name kmymoney \
#       kmymoney:latest

# Base docker image
FROM ubuntu:latest
LABEL maintainer "mongi3@gmail.com"

# NOTE: tango icons need to be enabled in kmymoney prefererences
#       as default system ones are half missing
# dbus-x11 is needed for kwalletd interaction
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive \
       apt-get install -y kmymoney \
       	       	       	  tango-icon-theme-common \
			  dbus-x11 \
    && apt-get clean

# Run unprivileged
RUN useradd --create-home --shell /bin/bash --groups audio kmymoney
USER kmymoney

# Suppress error
RUN mkdir -p /tmp/runtime-kmymoney && chmod 0700 /tmp/runtime-kmymoney
ENV XDG_RUNTIME_DIR=/tmp/runtime-kmymoney

ENTRYPOINT ["kmymoney"]
