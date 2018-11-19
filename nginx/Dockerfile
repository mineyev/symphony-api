FROM registry.mobbtech.com/common/ubuntu:16.04
LABEL authors "Evgeniy Mineyev <evgeniy.mineyev@iqoption.com>"

# Base layer
ENV TERM=xterm \
    LC_ALL=C.UTF-8 \
    DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get -y --no-install-recommends --no-install-suggests install software-properties-common \
        aptitude \
        apt-utils \
        nginx \
        curl \
        telnet \
        git

# Clean up
RUN apt-get autoremove -y && \
    apt-get autoclean -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm -rf /etc/nginx/sites-available /etc/nginx/sites/enabled

COPY ./.host /
COPY ./ /project/

RUN chmod +x /usr/local/sbin/consul.sh

WORKDIR /project

EXPOSE 80 443

CMD ["/usr/bin/supervisord", "-n"]