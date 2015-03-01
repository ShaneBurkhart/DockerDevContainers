FROM dockerfile/ubuntu

RUN apt-get update && apt-get -y install git mercurial meld 
RUN apt-get -y install vim tmux wget
RUN apt-get -y install docker.io

# Install docker-compose.  Python is installed, but why not install pip with it.
RUN \
    wget https://bootstrap.pypa.io/get-pip.py -O ~/get-pip.py && \
    python ~/get-pip.py && \
    rm ~/get-pip.py
RUN pip install -U docker-compose

ENV HOME /home
WORKDIR /home

VOLUME ["/home"]

CMD ["bash"]
