FROM  debian:stable

# 
RUN	apt-get update && yes | apt-get upgrade
RUN	apt-get install -y build-essential
RUN	apt-get -y install vim
RUN	apt-get -y install libsm6 libxext6 libxrender-dev
#
RUN	apt-get install -y python3 python3-pip

#
WORKDIR	/app
COPY	.	/app

#
RUN	ln -s /usr/bin/python3 /usr/bin/python
RUN	ln -s /usr/bin/pip3 /usr/bin/pip
RUN	pip install --upgrade pip

#install 
RUN	pip install numpy
RUN	pip install scikit-learn
RUN	pip install scipy
RUN	pip install matplotlib
RUN	pip install opencv-python
RUN	pip install jupyter

# required root password
RUN	jupyter notebook --generate-config --allow-root
RUN	echo "c.NotebookApp.password = u'sha1:6a3f528eec40:6e896b6e4828f525a6e20e5411cd1c8075d68619'" >> /root/.jupyter/jupyter_notebook_config.py

EXPOSE	8888
ENTRYPOINT	jupyter notebook --allow-root --ip=0.0.0.0 --port=8888 --no-browser

