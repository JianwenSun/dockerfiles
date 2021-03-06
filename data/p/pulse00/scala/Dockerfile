# Scala and sbt for Ubuntu 13.10  
#  
# Version 0.1  
FROM pulse00/java  
MAINTAINER Robert Gruendler r.gruendler@dubture.com  
  
# install add-apt-repository tool  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes software-
properties-common  
  
# install wget for downloading files  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes wget  
  
# Typesafe repo (contains old versions but they have all dependencies we need
later on)  
RUN wget http://apt.typesafe.com/repo-deb-build-0002.deb  
RUN dpkg -i repo-deb-build-0002.deb  
RUN rm -f repo-deb-build-0002.deb  
  
# update apt repositories  
RUN apt-get update  
  
# install Scala 2.10.3, requires OpenJDK 1.6  
# 1) first install prerequisites  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes
openjdk-6-jre libjansi-java  
# 2) finally install Scala 2.10.3  
RUN wget http://www.scala-lang.org/files/archive/scala-2.10.3.deb  
RUN dpkg -i scala-2.10.3.deb  
RUN rm -f scala-2.10.3.deb  
  
# install sbt 0.13.1  
# 1) first install old sbt 0.11.3 from typesafe (old one but comes with all
dependencies)  
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes sbt  
# 2) now that we have sbt we can upgrade it to 0.13.1  
RUN wget http://repo.scala-sbt.org/scalasbt/sbt-native-packages/org/scala-
sbt/sbt/0.13.1/sbt.deb  
RUN dpkg -i sbt.deb  
RUN rm -f sbt.deb  
  
# Set java 7 as default  
RUN update-alternatives --set java /usr/lib/jvm/java-7-oracle/jre/bin/java  
  
# fetches all sbt jars from Maven repo so that your sbt will be ready to be
used when you launch the image  
RUN sbt --version  
  
# Define default command.  
CMD ["scala"]  

