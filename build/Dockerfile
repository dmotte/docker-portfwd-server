# Tested with docker.io/library/alpine:3.22.0
FROM docker.io/library/alpine:latest

RUN apk add --no-cache openssh-server

COPY --chown=root:root --chmod=644 sshd_config /etc/ssh/

EXPOSE 22

RUN install -dm700 /ssh-host-keys /ssh-client-keys

COPY --chown=root:root --chmod=755 startup.sh /

ENTRYPOINT ["/startup.sh"]
