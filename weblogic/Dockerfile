# Use Centos 6 base Image
FROM vamsp7/centos6

# Maintainer of the image
MAINTAINER Victor Mejia Silva -> https://hub.docker.com/u/vamsp7 - https://hub.docker.com/u/vamsp7/

## JDK Installer
ADD /c/Users/VICTORMEJIA/Downloads/instaladores/jdk-7u71-linux-x64.rpm /tmp/installers/

## Weblogic12c Installer
ADD /c/Users/VICTORMEJIA/Downloads/instaladores/wls_121200.jar /tmp/installers/


#Install JDK 7
RUN rpm -Uvh /tmp/installers/jdk-7u71-linux-x64.rpm; \ 
yum -y install libXrender

# Oracle user for installation
RUN useradd -d /home/oracle oracle; \
echo oracle:oracle | chpasswd

# Weblogic12c Instalation
USER oracle

RUN git clone https://github.com/victor-mejia/dockerfiles.git /tmp/installations-resources; \ 
mkdir /home/oracle/inventory-directory; \
cp /tmp/installations-resources/oraInst.loc /home/oracle/oraInst.loc \
java -Xmx1024m -jar /tmp/installers/wls_121200.jar -silent -responseFile /tmp/installations-resources/responsefile.rsp -invPtrLoc /home/oracle/oraInst.loc

## Creación del dominio
/home/oracle/products/Oracle_Home/oracle_common/common/bin/wlst.sh /tmp/createDomain.py

# Expose ports SSH 22, SAMBA 138/udp 139 445/udp 445, WEBLOGIC 7006
EXPOSE 22
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445/udp
EXPOSE 445
EXPOSE 7006

# Start samba, ssh services and weblogic adminconsole
CMD service smb start; \
/usr/sbin/sshd -D; \
/home/oracle/products/Oracle_Home/user_projects/domains/base_domain/startWebLogic.sh

#Quickstart command:  
#docker run -d -p 1022:22 -p 138:138/udp -p 139:139 -p 445:445 -p 445:445/udp -p 7006:7006 -h centos-base --name centos-base [image name]
