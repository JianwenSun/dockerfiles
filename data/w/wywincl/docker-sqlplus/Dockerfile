FROM sflyr/ubuntu  
MAINTAINER sflyr  
  
RUN apt-get -y update  
RUN apt-get -y install libaio1 unzip rlwrap  
ADD instantclient-basic-linux.x64-11.2.0.3.0.zip /  
ADD instantclient-sqlplus-linux.x64-11.2.0.3.0.zip /  
ADD instantclient-sdk-linux.x64-11.2.0.3.0.zip /  
ADD instantclient-jdbc-linux.x64-11.2.0.3.0.zip /  
RUN unzip instantclient-basic-linux.x64-11.2.0.3.0.zip  
RUN unzip instantclient-sqlplus-linux.x64-11.2.0.3.0.zip  
RUN unzip instantclient-sdk-linux.x64-11.2.0.3.0.zip  
RUN unzip instantclient-jdbc-linux.x64-11.2.0.3.0.zip  
  
ENV NLS_LANG "SIMPLIFIED CHINESE_CHINA.WE8MSWIN1252"  
ENV LANG en_US.UTF-8  
ENV LD_LIBRARY_PATH instantclient_11_2  
  
# CMD /instantclient_11_2/sqlplus <user>/<password>@//xxx.yyy.eu-
west-1.rds.amazonaws.com:1521/ORCL  
CMD sleep 1; rlwrap /instantclient_11_2/sqlplus $URL  

