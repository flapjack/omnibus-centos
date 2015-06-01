FROM centos:centos7
MAINTAINER Jesse Reynolds @jessereynolds
# Original author: Derek Olsen in https://github.com/someword/omnibus-centos

#RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN rpm -ivh http://download.fedoraproject.org/pub/epel/7/$(arch)/e/epel-release-7-5.noarch.rpm
RUN yum groupinstall -y 'Development Tools'

RUN yum install -y \
    openssl-devel \
    expat-devel \
    perl-ExtUtils-MakeMaker \
    curl-devel \
    golang \
    tar \
    fakeroot \
    cmake \
    ruby \
    ruby-devel

RUN gem install bundler

# Work around git/go version issues on centos - https://twitter.com/gniemeyer/status/472318780472045568
RUN yum remove -y git

RUN cd /usr/src && \
    curl -o git-1.9.4.tar.gz https://www.kernel.org/pub/software/scm/git/git-1.9.4.tar.gz && \
    tar xzf git-1.9.4.tar.gz && cd git-1.9.4 && \
    make prefix=/usr all && make prefix=/usr install && \
    cd .. && rm -rf git-1.9.4.tar.gz git-1.9.4

RUN git config --global user.email "docker@flapjack.io" && \
    git config --global user.name "Flapjack Docker Packager"

RUN /bin/bash -l -c "git clone https://github.com/flapjack/omnibus-flapjack.git && cd omnibus-flapjack && bundle install --binstubs"
