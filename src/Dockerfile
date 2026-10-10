FROM alpine@sha256:294b683cb724975bec92580e1e685676bd4b50bda910ddb8c51d4cabeaec77e6

COPY named.conf /etc/bind/

RUN apk add --update-cache --no-cache bind
EXPOSE 53/udp

ENTRYPOINT ["/usr/sbin/named", "-f", "-g"]
