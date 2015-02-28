FROM dockerfile/ubuntu

RUN apt-get update && apt-get -y install git mercurial meld 
RUN apt-get -y install vim tmux wget
RUN apt-get -y install docker.io
RUN \
    git clone http://github.com/ShaneBurkhart/dotfiles.git ~/dotfiles && \
    cd ~/dotfiles && \
    ./makelinks.sh

CMD ["bash"]
