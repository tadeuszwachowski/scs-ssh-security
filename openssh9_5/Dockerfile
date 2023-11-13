FROM debian:latest as builder

USER root

# install openssl
RUN apt-get update && apt-get install -y curl tar build-essential autoconf automake util-linux 
RUN apt-get install -y openssl zlib1g-dev libssl-dev

WORKDIR /app

RUN curl -O https://artfiles.org/openbsd/OpenSSH/portable/openssh-9.5p1.tar.gz
RUN tar -xzf openssh-9.5p1.tar.gz
WORKDIR /app/openssh-9.5p1

# LAST
RUN ./configure
RUN make
RUN make install

FROM builder as final

RUN apt-get install -y netcat-openbsd
RUN useradd sshd

RUN set -ex \
    && adduser --home /home/example --shell /bin/bash --disabled-password --gecos "" example \
    && echo "example:123456" | chpasswd

EXPOSE 20022

CMD ["/usr/local/sbin/sshd", "-D"]
# CMD ["/bin/bash"]
# CMD ["/bin/bash"]
# CMD ["service","ssh","start"]
# CMD ["ssh","-V"]
