FROM airhacks/java
LABEL maintainer="Georg Henkel <info@georg-henkel.de>" description="Glassfish v5.0 with HypserSQL v2.4.0"

ENV GLASSFISH_ARCHIVE glassfish5
ENV HSQLDB_ARCHIVE hsqldb
ENV DOMAIN_NAME domain1
ENV INSTALL_DIR /

RUN curl -o ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip -L http://download.oracle.com/glassfish/5.0/release/glassfish-5.0.zip \ 
    && unzip ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip -d ${INSTALL_DIR} \ 
    && rm ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}.zip
    
ENV GLASSFISH_HOME ${INSTALL_DIR}/${GLASSFISH_ARCHIVE}/glassfish
ENV DEPLOYMENT_DIR ${GLASSFISH_HOME}/domains/${DOMAIN_NAME}/autodeploy
ENV LIB_DIR ${GLASSFISH_HOME}/domains/${DOMAIN_NAME}/lib/ext

COPY ./lib/hsqldb.jar ${LIB_DIR}

WORKDIR ${GLASSFISH_HOME}/bin
ENTRYPOINT asadmin start-domain --verbose ${DOMAIN_NAME}

EXPOSE 4848 8009 8080 8181