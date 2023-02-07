FROM ubuntu:22.04
RUN apt-get update && apt-get -y upgrade

# get the basics
RUN apt-get install -y curl git ssh build-essential

# add the sudo
RUN apt-get install sudo -y

# change the root password
RUN echo 'root:toor' | chpasswd

# create a user used for development
RUN useradd -ms /bin/bash devlh
# change the user password
RUN echo "devlh:testtest" | chpasswd
RUN adduser devlh sudo

# change the user
USER devlh
# change the workdir
WORKDIR /home/devlh

# configure git
RUN  git config --global --add safe.directory /workspaces/docu \
  && git config --global user.email "lucianhanga@gmx.net" \
  && git config --global user.name "Lucian Hanga"



