FROM ubuntu:latest
RUN apt-get update && \
    apt-get install -y git && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y maven && \
    apt-get install -y openssh-server

# Set SSH Configuration to allow remote logins without /proc write access
RUN sed -ri 's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd
# Add user jenkins to the image
RUN adduser --quiet jenkins
# Set password for the jenkins user 
RUN echo "jenkins:jenkins" | chpasswd
RUN mkdir /home/jenkins
RUN chown -R jenkins:jenkins /home/jenkins
# Standard SSH port
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]