# Use Centos 6 base Image
FROM vamsp7/centos6

# Maintainer of the image
MAINTAINER Victor Mejia Silva -> https://hub.docker.com/u/vamsp7 - https://hub.docker.com/u/vamsp7/

## JDK Installer
ADD jdk-7u71-linux-x64.rpm /tmp/installers/

## Weblogic12c Installer
ADD wls_121200.jar /tmp/installers/

#Install JDK 7
RUN rpm -Uvh /tmp/installers/jdk-7u71-linux-x64.rpm; \ 
yum -y install libXrender

# Oracle user for installation
RUN useradd -d /home/oracle oracle; \
echo oracle:oracle | chpasswd

# Weblogic12c Instalation
USER oracle

# If you notice that it takes a long time to create or update a domain using WLST
ENV CONFIG_JVM_ARGS=-Djava.security.egd=file:/dev/./urandom

RUN git clone https://github.com/victor-mejia/dockerfiles.git /tmp/installations-resources; \ 
mkdir /home/oracle/inventory-directory; \
java -Xmx1024m -jar /tmp/installers/wls_121200.jar -silent -responseFile /tmp/installations-resources/weblogic/responsefile.rsp -invPtrLoc /tmp/installations-resources/weblogic/oraInst.loc

## Creación del dominio
RUN /home/oracle/products/Oracle_Home/oracle_common/common/bin/wlst.sh /tmp/installations-resources/weblogic/createDomain.py

#Set user root by default
USER root

# Expose ports SSH 22, SAMBA 138/udp 139 445/udp 445, WEBLOGIC 7001
EXPOSE 22
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445/udp
EXPOSE 445
EXPOSE 7001

# Start samba, ssh services and weblogic adminconsole
CMD service smb start; \
service sshd start; \
runuser -l oracle -c '/home/oracle/products/Oracle_Home/user_projects/domains/base_domain/startWebLogic.sh'

#Quickstart command:  
#docker run -d -p 1022:22 -p 138:138/udp -p 139:139 -p 445:445 -p 445:445/udp -p 7001:7001 -h weblogic12c --name weblogic12c [image name]
