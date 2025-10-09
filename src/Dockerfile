FROM alpine@sha256:4b7ce07002c69e8f3d704a9c5d6fd3053be500b7f1c69fc0d80990c2ad8dd412

COPY named.conf /etc/bind/

RUN apk add --update-cache --no-cache bind
EXPOSE 53/udp

ENTRYPOINT ["/usr/sbin/named", "-f", "-g"]
