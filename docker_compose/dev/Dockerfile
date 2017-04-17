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
    tmux vim git unzip curl \
    && pip install --upgrade pip

# INSTALL GOSU
# https://github.com/tianon/gosu/blob/master/INSTALL.md
ENV GOSU_VERSION 1.10
RUN set -x \
	&& apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
	&& dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')" \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove ca-certificates wget

# DEFAULT COMMAND
CMD ["bash"]
