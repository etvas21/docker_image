FROM  ubuntu:18.04
LABEL maintainer="etvas21@naver.com"

ENV	DEBIAN_FRONTEND=noninteractive

# To test elasticsearch
RUN   apt-get update  \
      && apt-get install -y curl  \
		  && apt-get install -y wget  \
      && apt-get install -y vim

COPY  ko    /usr/ko
#RUN   sed -i '$ a\set encoding=utf-8' /etc/vim/vimrc
