FROM alpine:3.19

RUN apk add --update --no-cache bash && \
    apk add --update --no-cache docker && \
    # toutes les minutes
    echo "*       *       *       *       *       run-parts /etc/periodic/1min" >> /etc/crontabs/root

WORKDIR /