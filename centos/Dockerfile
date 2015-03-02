# Use Centos 6 base Image
FROM centos:6

# Maintainer of the image
MAINTAINER Victor Mejia Silva -> https://hub.docker.com/u/vamsp7 - https://hub.docker.com/u/vamsp7/

# Install the packages SSH, SAMBA, X11 and git
RUN yum -y install openssh-server openssh-clients samba samba-client samba-common xauth libXtst git

##Service configuration
RUN chkconfig sshd on; \
chkconfig smb on; \
chkconfig nmb on; \
git clone https://github.com/victor-mejia/installations-resources.git /tmp/installations-resources; \
cp /etc/samba/smb.conf /etc/samba/smb.conf.bak; \ 
cp /tmp/installations-resources/util/smb.conf /etc/samba/smb.conf; \
sed -i "s/.*PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config && sed -i "s/.*X11Forwarding.*/X11Forwarding yes/g" /etc/ssh/sshd_config

## Change root password
RUN echo root:admin123 | chpasswd

# Expose ports SSH 22 ; SAMBA 
EXPOSE 22
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445/udp
EXPOSE 445

# Start samba and ssh services 
CMD service smb start; \
/usr/sbin/sshd -D