# Use Centos 6 base Image
FROM vamsp7/centos6

# Maintainer of the image
MAINTAINER Victor Mejia Silva -> https://hub.docker.com/u/vamsp7 - https://hub.docker.com/u/vamsp7/

## JDK Installer
ADD jdk-8u45-linux-x64.rpm /tmp/installers/

## Weblogic12c Installer
ADD activator-1.3.4 /activator-1.3.4/

#Install JDK 8
RUN rpm -Uvh /tmp/installers/jdk-8u45-linux-x64.rpm; \ 
yum -y install libXrender; \
rm -rf /tmp/installers


# Expose ports SSH 22, SAMBA 138/udp 139 445/udp 445, Typesafe Activator 8888, Reactive Stocks App 9000
EXPOSE 22
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445/udp
EXPOSE 445
EXPOSE 8888
EXPOSE 9000

# Start samba, ssh services and activator
CMD service smb start; \
service sshd start; \
rm -f /RUNNING_PID; \ 
/activator-1.3.4/activator -Dhttp.address=0.0.0.0 ui

#Quickstart command:  
#docker run -d -p 1022:22 -p 138:138/udp -p 139:139 -p 445:445 -p 445:445/udp -p 8888:8888 -p 9000:9000 -h activator --name activator [image name]
