# The MIT License  
#  
# Copyright (c) 2015, CloudBees, Inc.  
#  
# Permission is hereby granted, free of charge, to any person obtaining a copy  
# of this software and associated documentation files (the "Software"), to
deal  
# in the Software without restriction, including without limitation the rights  
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
# copies of the Software, and to permit persons to whom the Software is  
# furnished to do so, subject to the following conditions:  
#  
# The above copyright notice and this permission notice shall be included in  
# all copies or substantial portions of the Software.  
#  
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM,  
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN  
# THE SOFTWARE.  
FROM openjdk:8-jdk  
LABEL MAINTAINER="Nicolas De Loof <nicolas.deloof@gmail.com>"  
  
ARG user=jenkins  
ARG group=jenkins  
ARG uid=1000  
ARG gid=1000  
ARG docker_version=17.05.0-ce  
ARG JENKINS_AGENT_HOME=/home/${user}  
  
ENV JENKINS_AGENT_HOME ${JENKINS_AGENT_HOME}  
  
RUN groupadd -g ${gid} ${group} \  
&& useradd -d "${JENKINS_AGENT_HOME}" -u "${uid}" -g "${gid}" -m -s /bin/bash
"${user}"  
  
# setup SSH server  
RUN apt-get update \  
&& apt-get install --no-install-recommends -y openssh-server \  
&& apt-get clean  
RUN sed -i 's/#PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config  
RUN sed -i 's/#RSAAuthentication.*/RSAAuthentication yes/'
/etc/ssh/sshd_config  
RUN sed -i 's/#PasswordAuthentication.*/PasswordAuthentication no/'
/etc/ssh/sshd_config  
RUN sed -i 's/#SyslogFacility.*/SyslogFacility AUTH/' /etc/ssh/sshd_config  
RUN sed -i 's/#LogLevel.*/LogLevel INFO/' /etc/ssh/sshd_config  
RUN mkdir /var/run/sshd  
  
RUN curl -vOL
"https://get.docker.com/builds/Linux/x86_64/docker-${docker_version}.tgz" \  
&& tar zxvf "docker-${docker_version}.tgz" \  
&& chmod +x docker/docker \  
&& mv docker/docker /usr/bin/ \  
&& rm -rf docker*  
  
#VOLUME "${JENKINS_AGENT_HOME}" "/tmp" "/run" "/var/run"  
WORKDIR "${JENKINS_AGENT_HOME}"  
  
COPY setup-sshd /usr/local/bin/setup-sshd  
  
EXPOSE 22  
ENTRYPOINT ["setup-sshd"]  

