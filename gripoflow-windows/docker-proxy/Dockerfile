FROM alpine:3.20

RUN apk add --no-cache socat

ENTRYPOINT ["socat"]
CMD ["TCP-LISTEN:2375,fork,reuseaddr", "UNIX-CONNECT:/var/run/docker.sock"]
