FROM docker.io/bitnami/minideb:bullseye

RUN apt-get -qq update && \
    apt-get -qq install -y curl make build-essential libapr1-dev libaprutil1-dev libpcre2-dev

WORKDIR /workspace

ARG HTTPD_VERSION=2.4.54
RUN curl -s https://dlcdn.apache.org/httpd/httpd-${HTTPD_VERSION}.tar.gz | tar -xz --strip-components 1
RUN ./configure --prefix=/opt/bitnami/apache --enable-mpms-shared=all

RUN make -j $(nproc)
RUN make install

ENV PATH="/opt/bitnami/apache/bin:${PATH}"

CMD [ "httpd", "-D", "FOREGROUND" ]
