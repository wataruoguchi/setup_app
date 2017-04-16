FROM ubuntu:16.04
MAINTAINER Wataru Oguchi

# SETUP SHARED DIR
RUN mkdir /src
ADD ./app/src /src/
RUN mkdir /config
ADD ./app/requirements.txt /config/
WORKDIR /src

# INSTALL PACKAGES FOR APP DEVELOPMENT
RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y python python3.5 python-pip python3-pip \
    nodejs npm \
    tmux vim git unzip \
    && pip install --upgrade pip

# DEFAULT COMMAND
CMD ["bash"]
