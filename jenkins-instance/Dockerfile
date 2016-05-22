FROM jenkins:latest

USER root
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y maven haveged

# Install let's encrypt certbot, this might need to be adjusted according to https://certbot.eff.org/
RUN apt-get install -y letsencrypt -t jessie-backports \
	&& letsencrypt --version \
	&& mkdir /var/jenkins_home/etc_letsencrypt \
	&& chown 1000:000 /var/jenkins_home/etc_letsencrypt \
	&& ln -s /var/jenkins_home/etc_letsencrypt /etc/letsencrypt \
	&& mkdir /var/jenkins_home/var_lib_letsencrypt \
	&& chown 1000:000 /var/jenkins_home/var_lib_letsencrypt \
	&& ln -s /var/jenkins_home/var_lib_letsencrypt /var/lib/letsencrypt \
	&& mkdir /var/jenkins_home/var_log_letsencrypt \
	&& chown 1000:000 /var/jenkins_home/var_log_letsencrypt \
	&& ln -s /var/jenkins_home/var_log_letsencrypt /var/log/letsencrypt

USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# See https://wiki.jenkins-ci.org/display/JENKINS/Starting+and+Accessing+Jenkins#StartingandAccessingJenkins-CommandLineParameters
ENV JENKINS_OPTS --httpPort=-1 --httpsPort=8443 --ajp13Port=-1