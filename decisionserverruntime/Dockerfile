FROM websphere-liberty:8.5.5.9-webProfile7
ARG ODMDOCKERDIR
MAINTAINER Laurent GRATEAU <laurent.grateau@fr.ibm.com>
ENV APP_NAME DecisionService
ENV ODMDOCKERDIR $ODMDOCKERDIR
ENV CONNECTION_POOL_SIZE 20
ENV SCRIPT /script
RUN mkdir /config/resources && \
	mkdir -p $SCRIPT && \
	mkdir -p /config/apps/extract
COPY $ODMDOCKERDIR/decisionserverruntime/script $SCRIPT
COPY $ODMDOCKERDIR/decisionserverruntime/server.xml /config/
COPY $ODMDOCKERDIR/dbdriver/derbyclient.jar /config/resources
COPY ./executionserver/applicationservers/WLP855/DecisionService.war /config/apps/

RUN cd /config/apps/extract && \ 
    unzip ../DecisionService.war && \
	cd ../ && \
    rm -rf DecisionService.war && \
    mv extract DecisionService.war && \
    cd /config/apps/DecisionService.war && \
    chmod -R a+x $SCRIPT
EXPOSE 9080

CMD ["/script/runds.sh"]
