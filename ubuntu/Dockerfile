FROM ubuntu:latest
MAINTAINER Ted Zlatanov <tzz@lifelogs.com>

LABEL classification=cfengine-docker-testbed
LABEL platform=ubuntu

# Use a locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Setup
RUN apt-get update -y
RUN apt-get install -y git curl whois procps etckeeper hostname findutils apt-transport-https
RUN /usr/bin/git config --global user.name "Root Tester"
RUN /usr/bin/git config --global user.email root@cfengine.docker.testbed.lan

ADD etckeeper.conf /etc/etckeeper/etckeeper.conf

RUN etckeeper init
RUN curl -s https://cfengine-package-repos.s3.amazonaws.com/pub/gpg.key | apt-key add -
ADD cfengine-community.list /etc/apt/sources.list.d/cfengine-community.list
RUN apt-get update -y
# Perl Data::Dumper is required
RUN apt-get install -y cfengine-community
RUN rm -f /var/cfengine/ppkeys/*
RUN #(nop) invalidate from here.......
ADD cfengine-tester /opt/local/bin/
CMD /opt/local/bin/cfengine-tester
