FROM jboss/base-jdk:7

# Switch back to root
USER root

# Install ssh server
RUN yum -y install openssh-server && yum clean all
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''

# Create Jenkins user and Jenkins group
RUN groupadd -r jenkins -g 1001 && useradd -u 1001 -r -g jenkins -m -d /opt/jenkins -s /bin/bash -c "Jenkins user" jenkins
RUN echo "jenkins:jenkins" | chpasswd

# Set the working directory to jenkins' user home directory
WORKDIR /opt/jenkins

# Expose standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
