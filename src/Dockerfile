FROM alpine@sha256:4bcff63911fcb4448bd4fdacec207030997caf25e9bea4045fa6c8c44de311d1

COPY named.conf /etc/bind/

RUN apk add --update-cache --no-cache bind
EXPOSE 53/udp

ENTRYPOINT ["/usr/sbin/named", "-f", "-g"]
