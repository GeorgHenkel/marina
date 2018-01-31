FROM openjdk:8u151-jre-alpine3.7
MAINTAINER Georg Henkel <info@georg-henkel.de> (@Georg_Henkel)

RUN apk update \
  && apk add ca-certificates \
  && update-ca-certificates \
  && apk add openssl

# Install WebSphere Liberty
ENV LIBERTY_VERSION 2018.1.0.0
RUN wget https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/wlp-beta-${LIBERTY_VERSION}.zip -O /tmp/wlp-beta.zip \
    && mkdir -p /opt/ibm \
    && unzip -q /tmp/wlp-beta.zip -d /opt/ibm \
    && rm /tmp/wlp-beta.zip
ENV PATH=/opt/ibm/wlp/bin:$PATH

# Set Path Shortcuts
ENV LOG_DIR=/logs
ENV WLP_OUTPUT_DIR=/opt/ibm/wlp/output
ENV SERVER_NAME=javaee8
RUN mkdir /logs \
    && server create ${SERVER_NAME} \
    && ln -s $WLP_OUTPUT_DIR/${SERVER_NAME} /output \
    && ln -s /opt/ibm/wlp/usr/servers/${SERVER_NAME} /config \
    && rm -rf $WLP_OUTPUT_DIR/.classCache /output/workarea

COPY server.xml /opt/ibm/wlp/usr/servers/${SERVER_NAME}/
EXPOSE 9080 9443

CMD server run $SERVER_NAME
