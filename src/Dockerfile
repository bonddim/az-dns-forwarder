FROM alpine@sha256:25109184c71bdad752c8312a8623239686a9a2071e8825f20acb8f2198c3f659

COPY named.conf /etc/bind/

RUN apk add --update-cache --no-cache bind
EXPOSE 53/udp

ENTRYPOINT ["/usr/sbin/named", "-f", "-g"]
