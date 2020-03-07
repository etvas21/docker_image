##############################################
#	Dockerfile to create Python3.7 image
#   docker build -t py3_nlp:3.7 .
#   docker run -d -p 8888:8888 -v /Users/hrkim/database/docker_volume/app_nlp:/app py3_nlp:3.7
#   localhost:8888
#
#	NLP environement
#		gensim, nltk, konlpy
##############################################

FROM  ubuntu:18.04
MAINTAINER	HRKIM <etvas21@naver.com>

#
RUN		apt-get update  \
    	&& apt-get upgrade \
      	&& apt-get install -y curl  \
	  	&& apt-get install -y wget  \
      	&& apt-get install -y vim  \
      	&& apt-get install -y software-properties-common \
    	&& apt-get install -y build-essential vim python3.7 python3-pip

# In order to enter Hangul
RUN   sed -i '$ a\set encoding=utf-8' /etc/vim/vimrc


# Copy data
COPY    punkt                         /root/nltk_data/tokenizers/punkt
COPY    averaged_perceptron_tagger    /root/nltk_data/taggers/averaged_perceptron_tagger
#################
#COPY	data	                      /app/data
#COPY	src	                          /app/src
#COPY	model	                      /app/model
#################
COPY    requirements.txt              /app/

WORKDIR	/app


############################################################
# To install Java
############################################################
# Add the "JAVA" ppa
# and Install OpenJDK-8
# Fix certificate issues
RUN 	add-apt-repository -y ppa:webupd8team/java \
    	&& apt-get install -y openjdk-8-jdk \
    	&& apt-get install -y ant \
    	&& apt-get clean \
    	&& apt-get install ca-certificates-java \
    	&& apt-get clean \
    	&& update-ca-certificates -f

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

############################################################
# To install Python package
############################################################
#RUN apt-get(Advanced packaging Tool)
RUN		pip3 install -r requirements.txt	\
		&& pip3 install tensorflow==2.0.0a0	\
        #&& pip3 install --upgrade tensorflow	\
        && pip3 install pandas_profiling    \
        && pip3 install scipy				\
		&& pip3 install PyMySQL				\
		&& pip3 install elasticsearch		\
        ####
		&& pip3 install gensim				\
		&& pip3 install nltk				\
		&& pip3 install jpype1				\
		&& pip3 install konlpy
#
RUN		ln -s /usr/bin/python3 /usr/bin/python
RUN		ln -s /usr/bin/pip3 /usr/bin/pip
RUN     pip install --upgrade pip

# required root password
#RUN	jupyter notebook --generate-config --allow-root
RUN		jupyter notebook --generate-config --allow-root --NotebookApp.token=''
RUN		echo "c.NotebookApp.password = u'sha1:6a3f528eec40:6e896b6e4828f525a6e20e5411cd1c8075d68619'" >> /root/.jupyter/jupyter_notebook_config.py

EXPOSE	8888

# There can only be one CMD instruction in a Dockerfile.
# If you list more than one CMD then only the last CMD will take effect.
# ref:https://docs.docker.com/engine/reference/builder/
# Not work
#CMD	["mkdir", "./data", "./src"]
ENTRYPOINT	jupyter notebook --allow-root --ip=0.0.0.0 --port=8888 --no-browser


#########################################################################
# To do
#########################################################################
# [done]Create sub-folders /app/data, /app/src
# change login pasword
# [done]run as docker-compose
### end of script ###
