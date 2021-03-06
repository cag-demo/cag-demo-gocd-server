# Dockerfile for ThoughtWorks Go Server Agent (http://www.go.cd)
#
# Inspired by:
# http://github.com/patforna/docker/go-server
# http://www.go.cd/2014/05/18/manage-agents-with-docker.html

FROM maven:3-jdk-8
MAINTAINER Mikael Sennerholm <mikael@sennerholm.net>

# Download and install Go-agent 15.1.0, curl/git/jq and docker, totum
# http://download.go.cd/gocd-deb/go-agent-15.1.0-1863.deb
# new url https://download.go.cd/binaries/15.2.0-2248/deb/go-agent-15.2.0-2248.deb
RUN wget -O /tmp/go-agent.deb https://download.go.cd/binaries/15.2.0-2248/deb/go-agent-15.2.0-2248.deb && \
	dpkg -i /tmp/go-agent.deb && \
	rm -f /tmp/go-agent.deb && \
  	apt-get install -y curl git && \
    curl -sSL https://get.docker.com/ | sh && \
    apt-get install -y --force-yes python-pip jq docker-engine=1.9.1-0~jessie && \
    pip install docker-cloud && \
  	apt-get clean # Clean up


# Add maven settings
# COPY maven-settings.xml /root/.m2/settings.xml moved to godata
COPY autoregister.properties /var/lib/go-agent/config/autoregister.properties
COPY go-agent /etc/default/go-agent

# This should probably be something like supervisord to keep the container running
CMD /usr/share/go-agent/agent.sh && tail -F /var/log/go-agent/go-agent.log
