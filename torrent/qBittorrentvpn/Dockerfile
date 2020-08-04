FROM ubuntu:18.04

# set environment variables
ENV DEBIAN_FRONTEND noninteractive

RUN usermod -u 99 nobody

RUN \
  echo "**** install packages ****" && \
  apt-get update && \
  apt-get install -y --no-install-recommends apt-utils openssl && \
  apt-get install -y software-properties-common && \
  echo "**** install qbittorrent & openvpn ****" && \
  add-apt-repository ppa:qbittorrent-team/qbittorrent-stable && \
  apt-get update && \
  apt-get install -y qbittorrent-nox openvpn curl moreutils net-tools dos2unix kmod iptables ipcalc unrar && \
  echo "**** cleanup ****" && \
  apt-get clean && \
  rm -rf \
         /var/lib/apt/lists/* \
         /tmp/* \
         /var/tmp/*

# volumes
VOLUME /config /downloads

# add configuration and scripts
COPY root/ /

RUN chmod +x /etc/qbittorrent/*.sh /etc/qbittorrent/*.init /etc/openvpn/*.sh

# ports
EXPOSE 8080
EXPOSE 8999
EXPOSE 8999/udp
CMD ["/bin/bash", "/etc/openvpn/start.sh"]
