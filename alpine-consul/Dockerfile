FROM alpine:3.7

ENV BUILD_DEPS="gettext"  \
    RUNTIME_DEPS="libintl"

# Download and install curl, envusbst
RUN set -x && \
    apk upgrade --update --no-cache && \
    apk add --update $RUNTIME_DEPS && \
    apk add --virtual build_deps $BUILD_DEPS &&  \
    apk add --update --no-cache curl && \
    cp /usr/bin/envsubst /usr/local/bin/envsubst && \
    apk del build_deps


ENV CONSUL_TEMPLATE_VERSION=0.19.0

# Download and install Consul Template
ADD https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip \
    /tmp/consul-template.zip
RUN set -x && \
    unzip -d /usr/sbin/ /tmp/consul-template.zip && \
    rm /tmp/consul-template.zip


COPY ./.host /
RUN chmod +x /usr/local/sbin/consul-register.sh