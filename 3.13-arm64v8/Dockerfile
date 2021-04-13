# buildkit bug workaround - https://github.com/moby/buildkit/issues/1368
FROM arm64v8/alpine:3.13

ENV GLIBC_VERSION 2.32-r0

RUN \
   apk add --update curl && \
   curl -Lo glibc.apk "https://github.com/ljfranklin/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}-arm64/glibc-${GLIBC_VERSION}.apk" && \
   curl -Lo glibc-bin.apk "https://github.com/ljfranklin/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}-arm64/glibc-bin-${GLIBC_VERSION}.apk" && \
   apk add --allow-untrusted glibc-bin.apk glibc.apk && \
   /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib && \
   echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf && \
   apk del curl && \
   rm -rf glibc.apk glibc-bin.apk /var/cache/apk/*
