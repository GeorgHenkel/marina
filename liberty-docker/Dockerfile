FROM openjdk:8u151-jre-alpine3.7
LABEL maintainer="Georg Henkel, <info@georg-henkel.de> (@Georg_Henkel)" description="OpenLiberty Java EE 8 and DerbyDB"

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
ENV SERVER_NAME=javaee8
ENV APPLICATION_DIR /opt/ibm/wlp/usr/servers/${SERVER_NAME}
ENV DEPLOYMENT_DIR ${APPLICATION_DIR}/dropins

RUN mkdir /logs \
    && server create ${SERVER_NAME} \
    && ln -s /opt/ibm/wlp/output/${SERVER_NAME} /output \
    && ln -s ${APPLICATION_DIR} /config \
    && rm -rf /opt/ibm/wlp/output/.classCache /output/workarea

COPY server.xml ${APPLICATION_DIR}/

RUN mkdir -p /opt/lib/jdbc/derby \
    && mkdir -p /opt/databases
	
COPY derby/derby.jar /opt/lib/jdbc/derby/

EXPOSE 9080 9443

CMD server run $SERVER_NAME