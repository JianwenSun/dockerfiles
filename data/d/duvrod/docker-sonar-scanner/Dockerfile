  
FROM java:8  
RUN apt-get update  
RUN apt-get install -y curl  
RUN apt-get install -y git  
RUN apt-get install -y tmux  
RUN apt-get install -y htop  
RUN apt-get install -y maven  
  
# Don't need these right now. Java is covered in the FROM statement above,  
# and build-essential might be overkill for now.  
# RUN sudo apt-get install -y openjdk-7-jdk  
# RUN sudo apt-get install -y build-essential  
# Set timezone to CST  
ENV TZ=America/Chicago  
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone  
  
WORKDIR /root  
  
RUN curl --insecure -OL https://sonarsource.bintray.com/Distribution/sonar-
scanner-cli/sonar-scanner-2.8.zip  
RUN unzip sonar-scanner-2.8.zip  
RUN rm sonar-scanner-2.8.zip  
  
ENV SONAR_RUNNER_HOME=/root/sonar-scanner-2.8  
ENV PATH $PATH:/root/sonar-scanner-2.8/bin  
  
COPY sonar-runner.properties ./sonar-scanner-2.8/conf/sonar-runner.properties  
  
# Use bash if you want to run the environment from inside the shell, otherwise
use the command that actually runs the underlying stuff  
#CMD /bin/bash  
CMD sonar-runner -Dsonar.projectBaseDir=./src  

