FROM ubuntu:22.04

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y curl git ssh build-essential

RUN  git config --global --add safe.directory /workspaces/docu \
  && git config --global user.email "lucianhanga@gmx.net" \
  && git config --global user.name "Lucian Hanga"



