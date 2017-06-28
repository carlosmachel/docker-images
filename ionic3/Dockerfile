FROM ubuntu:16.04

MAINTAINER Carlos Machel <carlosmachel@users.noreply.github.com>

ARG MYUSERNAME=developer
ARG MYUID=2000
ARG MYGID=200

ENV DEBIAN_FRONTEND=noninteractive \
    ANDROID_HOME=/opt/android-sdk-linux \
    NODE_VERSION=6.10.3 \
    NPM_VERSION=5.0.1 \
    IONIC_VERSION=3.3.0 \
    CORDOVA_VERSION=7.0.0 \
    MYUSERNAME=${MYUSERNAME} \
    MYUID=${MYUID} \
    MYGID=${MYGID} 

#BASIC STUFF
RUN apt-get update \ 
    && apt-get install -y --fix-missing \
    sudo python-software-properties software-properties-common build-essential git wget curl unzip ruby \
    && git config --global user.email "carlosmachel@users.noreply.github.com" \
    && git config --global user.name "Carlos Machel" \
    && curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh \
    && bash nodesource_setup.sh \
    && apt-get install -y nodejs \
    && npm config set unsafe-perm true --global \
    && npm install -g npm@latest \    
    && npm install -g cordova@"$CORDOVA_VERSION" ionic@"$IONIC_VERSION" \
    && gem install sass \
    && ionic start myApp sidemenu

RUN echo 'Creating user: ${MYUSERNAME} wit UID $UID'

RUN mkdir -p /home/${MYUSERNAME}

RUN echo "${MYUSERNAME}:x:${MYUID}:${MYGID}:Developer,,,:/home/${MYUSERNAME}:/bin/bash" >> /etc/passwd

RUN echo "${MYUSERNAME}:x:${MYGID}:" >> /etc/group 

RUN sudo echo "${MYUSERNAME} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/${MYUSERNAME}

RUN sudo chmod 0440 /etc/sudoers.d/${MYUSERNAME} 

RUN sudo chown ${MYUSERNAME}:${MYUSERNAME} -R /home/${MYUSERNAME} 

RUN sudo chown root:root /usr/bin/sudo 

RUN chmod 4755 /usr/bin/sudo 

WORKDIR myApp
EXPOSE 8100 35729
CMD ["ionic", "lab"]
