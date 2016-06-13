FROM alpine:3.2

RUN ALPINE_GLIBC_VERSION="2.23-r2" && \
    ALPINE_GLIBC_URL="https://github.com/sgerrand/alpine-pkg-glibc/releases/download/$ALPINE_GLIBC_VERSION" && \
    GLIBC_PKG="glibc-$ALPINE_GLIBC_VERSION.apk" && \
    GLIBC_BIN_PKG="glibc-bin-$ALPINE_GLIBC_VERSION.apk" && \
    GLIBC_I18N_PKG="glibc-i18n-$ALPINE_GLIBC_VERSION.apk" && \
    DOCKERIZE_VERSION="0.2.0" && \
    DOCKERIZE_URL="https://github.com/jwilder/dockerize/releases/download/v$DOCKERIZE_VERSION" && \
    DOCKERIZE_PKG="dockerize-linux-amd64-v$DOCKERIZE_VERSION.tar.gz" && \
    apk add --update -t deps wget ca-certificates curl bash && \
    cd /tmp && \
    curl -L $ALPINE_GLIBC_URL//$GLIBC_PKG -o $GLIBC_PKG && \
    curl -L $ALPINE_GLIBC_URL/$GLIBC_BIN_PKG -o $GLIBC_BIN_PKG && \
    curl -L $ALPINE_GLIBC_URL/$GLIBC_I18N_PKG -o $GLIBC_I18N_PKG && \
    apk add --allow-untrusted $GLIBC_PKG $GLIBC_BIN_PKG $GLIBC_I18N_PKG && \
    /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true && \
    echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
    curl -L $DOCKERIZE_URL/$DOCKERIZE_PKG -o $DOCKERIZE_PKG && \
    tar -C /usr/local/bin -xzvf $DOCKERIZE_PKG && \
    apk del --purge deps glibc-i18n && \
    apk add --update wget ca-certificates curl bash && \
    rm -rf /tmp/* /var/cache/apk/*
