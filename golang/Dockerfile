FROM shaneburkhart/dev

# Install GoLang
ENV GOLANG_VERSION 1.4.2

RUN wget -O ~/go.tar.gz https://storage.googleapis.com/golang/go${GOLANG_VERSION}.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf ~/go.tar.gz
RUN rm ~/go.tar.gz

RUN mkdir -p /go/src
RUN mkdir -p /go/bin
RUN mkdir -p /go/pkg

RUN echo "export PATH=\$PATH:/usr/local/go/bin" >> ~/.bashrc
RUN echo "export GOPATH=/go" >> ~/.bashrc
RUN echo "export PATH=\$PATH:\$GOPATH/bin" >> ~/.bashrc

WORKDIR /go
