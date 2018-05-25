FROM debian:jessie
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root

RUN apt-get update                                                                                                               \
    && apt-get upgrade -qy             

RUN apt-get install -qy curl


#################################
################################
# TBD Down to the entrypoint
# Install gosu for user mapping
# Needed for the entrypoint.sh script
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN    curl -o /usr/local/bin/gosu --insecure -SL "https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture)" \
    && curl -o /usr/local/bin/gosu.asc --insecure -SL "https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture).asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu
################################3
###################################33

## Needed by poky 
RUN apt-get install -qy python3

## Needed by python 
RUN apt-get install locales && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8

## Needed by bitbake
RUN apt-get install -yq bzip2 chrpath cpio cpp diffstat g++ gawk gcc git make patch python wget

# Install go
#RUN wget -qO- https://dl.google.com/go/go1.10.2.linux-amd64.tar.gz | tar -xz -C /usr/local

# Install qemu
#COPY usr/bin/qemu-arm-static /usr/bin/qemu-arm-static


# final setup
WORKDIR /source

ENV PATH /usr/local/go/bin:$PATH
ENV GOPATH /source/go

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["bash"]
