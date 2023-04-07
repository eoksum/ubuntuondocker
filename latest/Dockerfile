FROM       ubuntu:latest
MAINTAINER eoksum "https://github.com/eoksum/ubuntuondocker"

ENV LANG C.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends lsb-core openssh-server cron wget curl git vim nano sudo ca-certificates mtr

RUN mkdir /var/run/sshd \
mkdir /var/run/cron

ADD init.sh /
ADD geotr_id_rsa /root/.ssh/id_rsa
ADD geotr_id_rsa.pub /root/.ssh/id_rsa.pub

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/^#?PasswordAuthentication\s+.*/PasswordAuthentication no/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -i '$a\export LANG=C.UTF-8' /etc/profile

RUN mkdir /root/.ssh

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22

RUN chmod 755 ./init.sh
CMD ["/init.sh"]