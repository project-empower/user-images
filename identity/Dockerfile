FROM alpine


# gpg agent socket located at /identity/gnupg/agent-socket
RUN apk add gnupg
RUN apk add openssh-server
RUN apk add avahi

RUN apk add openssh-client

RUN ssh-keygen -A

RUN echo "[Server]" >> /etc/avahi/avahi-daemon.conf
RUN echo "enable-dbus=no" >> /etc/avahi/avahi-daemon.conf

RUN echo "PubKeyAuthentication yes" > /etc/ssh/sshd_config
RUN echo "StreamLocalBindUnlink yes" >> /etc/ssh/sshd_config
#RUN echo "AllowStreamLocalForwarding yes" >> /etc/ssh/sshd_config

#RUN ssh-keygen -A

#RUN echo "AllowTcpForwarding yes" >> /etc/ssh/sshd_config

#RUN apk add man

COPY init-script /init-script

RUN addgroup -S -g 1000 identity \
  && adduser -h /identity -u 1000 -G identity -D identity \
  && passwd -u identity

ENTRYPOINT ["sh", "/init-script"]
