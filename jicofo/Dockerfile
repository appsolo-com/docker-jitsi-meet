ARG JITSI_REPO=jitsi
ARG BASE_TAG=latest
FROM ${JITSI_REPO}/base-java:${BASE_TAG}

LABEL org.opencontainers.image.title="Jitsi Conference Focus (jicofo)"
LABEL org.opencontainers.image.description="Server-side focus component that manages media sessions and acts as load balancer."
LABEL org.opencontainers.image.url="https://github.com/jitsi/jicofo"
LABEL org.opencontainers.image.source="https://github.com/jitsi/docker-jitsi-meet"
LABEL org.opencontainers.image.documentation="https://jitsi.github.io/handbook/"

ENV BUILD_NUMBER 1
ENV EMAIL "grant@appsolo.com"

RUN apt-dpkg-wrap apt-get update \
    # apt-dpkg-wrap apt-get install -y jicofo && \
    && apt-get -y install git wget unzip devscripts \
    && apt-get -y install default-jdk ant maven debhelper build-essential \
    && apt-cleanup

RUN git clone https://github.com/jitsi/jicofo.git focus
WORKDIR /focus
RUN git checkout $JICOFO_TAG \
    && wget -O lib/maven-ant-tasks-2.1.3.jar https://repo.maven.apache.org/maven2/org/apache/maven/maven-ant-tasks/2.1.3/maven-ant-tasks-2.1.3.jar
RUN mvn dependency:resolve
RUN resources/build_deb_package.sh
    # && unzip dist/linux/jicofo-linux-x64-build.SVN.zip

COPY rootfs/ /

VOLUME /config
