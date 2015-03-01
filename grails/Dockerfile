FROM shaneburkhart/dev:java

# Install Grails
ENV GRAILS_VERSION 2.4.4

WORKDIR /usr/lib/jvm
RUN \
    wget http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-${GRAILS_VERSION}.zip && \
    unzip grails-${GRAILS_VERSION}.zip && \
    rm -rf grails-${GRAILS_VERSION}.zip && \
    ln -s grails-${GRAILS_VERSION} grails

ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

WORKDIR /home
