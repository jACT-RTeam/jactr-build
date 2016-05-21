FROM jenkins:latest

USER root
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y maven

USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# See https://wiki.jenkins-ci.org/display/JENKINS/Starting+and+Accessing+Jenkins#StartingandAccessingJenkins-CommandLineParameters
ENV JENKINS_OPTS --httpPort=-1 --httpsPort=8443 --ajp13Port=-1