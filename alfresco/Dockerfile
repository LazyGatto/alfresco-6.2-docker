FROM alfresco/alfresco-content-repository-community:6.1.2-ga

# Add services configuration to alfresco-global.properties
RUN echo -e '\n\
alfresco.host=ecm.egorod.info\n\
alfresco.port=443\n\
alfresco.protocol=https\n\
\n\
share.host=ecm.egorod.info\n\
share.port=443\n\
share.protocol=https\n\
\n\
ftp.enabled=true\n\
ftp.port=2121\n\
\n\
imap.server.enabled=true\n\
imap.server.port=1143\n\
\n\
email.server.enabled=true\n\
email.server.port=2525\n\
\n\
cifs.enabled=true\n\
cifs.tcpipSMB.port=1445\n\
cifs.netBIOSSMB.namePort=1137\n\
cifs.netBIOSSMB.datagramPort=1138\n\
cifs.netBIOSSMB.sessionPort=1139\n\
\n\
' >> /usr/local/tomcat/shared/classes/alfresco-global.properties

# Extra software
RUN set -x \
	&& yum install -y \
	wget \
	unzip \
	&& yum clean all

# Install api-explorer webapp for REST API
RUN set -x \
    && wget https://artifacts.alfresco.com/nexus/service/local/repositories/releases/content/org/alfresco/api-explorer/6.0.7-ga/api-explorer-6.0.7-ga.war -O /usr/local/tomcat/webapps/api-explorer.war

ARG TOMCAT_DIR=/usr/local/tomcat

RUN mkdir -p $TOMCAT_DIR/amps

# Install modules and addons
COPY modules/jars $TOMCAT_DIR/webapps/alfresco/WEB-INF/lib

#RUN java -jar $TOMCAT_DIR/alfresco-mmt/alfresco-mmt*.jar install $TOMCAT_DIR/amps $TOMCAT_DIR/webapps/alfresco -directory -nobackup -force

EXPOSE 2121 1143 2525 1445 1137/udp 1138/udp 1139
