
# Pull base image.
FROM ubuntu:16.04

LABEL maintainer "Naveen Tak"

LABEL "ProductName"="Mule EE Runtime with Mongo" \
    "ProductVersion"="4.1"

# Install curl
RUN apt-get update && \
    apt-get install unzip && \
    apt-get install -y --no-install-recommends locales && \
    locale-gen en_US.UTF-8 && \
    apt-get dist-upgrade -y && \
    apt-get --purge remove openjdk* && \
    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
    apt-get update && \
    apt-get install -y --no-install-recommends oracle-java8-installer oracle-java8-set-default && \
    apt-get clean all

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


# Copy mule zip, extract & install and run mule runtime
COPY mule-ee-distribution-standalone-4.1.2.zip /opt

RUN mkdir -p /opt && \
    cd /opt && \
    unzip mule-ee-distribution-standalone-4.1.2.zip && \
    rm mule-ee-distribution-standalone-4.1.2.zip && \
    mv mule-enterprise-standalone-4.1.2 mule && \
    cd mule/bin

# Deploy bar
COPY personapi.jar /opt/mule/apps/

#Expose default admin port and http port
EXPOSE 8081

#Run mule and mongo
CMD /opt/mule/bin/./mule start