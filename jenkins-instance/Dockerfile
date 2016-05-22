FROM jenkins:latest

USER root
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y maven haveged

# Install let's encrypt certbot, this might need to be adjusted according to https://certbot.eff.org/
RUN apt-get install -y letsencrypt -t jessie-backports

USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# See https://wiki.jenkins-ci.org/display/JENKINS/Starting+and+Accessing+Jenkins#StartingandAccessingJenkins-CommandLineParameters
ENV JENKINS_OPTS --httpPort=-1 --httpsPort=8443 --ajp13Port=-1