from maven:3.5.0-jdk-8-alpine  
  
MAINTAINER doublebyte <joana.simoes@geocat.net>  
  
#ARG INSTALL_ETF_PATH  
#ARG INSTALL_DASHBOARD_PATH  
ENV INSTALL_ETF_PATH /var/local/etf  
ENV INSTALL_DASHBOARD_PATH /daobs-data-dir  
  
ENV CATALINA_HOME /usr/local/tomcat  
ENV PATH $CATALINA_HOME/bin:$PATH  
RUN mkdir -p "$CATALINA_HOME"  
WORKDIR $CATALINA_HOME  
  
# From tomcat:8.5.16-jre8-alpine  
# let "Tomcat Native" live somewhere isolated  
ENV TOMCAT_NATIVE_LIBDIR $CATALINA_HOME/native-jni-lib  
ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH:+$LD_LIBRARY_PATH:}$TOMCAT_NATIVE_LIBDIR  
  
RUN apk add --update nodejs nodejs-npm && npm install npm@latest -g  
RUN apk add --no-cache gnupg git  
  
# see https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/KEYS  
# see also "update.sh" (https://github.com/docker-
library/tomcat/blob/master/update.sh)  
ENV GPG_KEYS 05AB33110949707C93A279E3D3EFE6B686867BA6
07E48665A34DCAFAE522E5E6266191C37C037D42
47309207D818FFD8DCD3F83F1931D684307A10A5
541FBE7D8F78B25E055DDEE13C370389288584E7
61B832AC2F1C5A90F0F9B00A1C506407564C17A3
713DA88BE50911535FE716F5208B0AB1D63011C7
79F7026C690BAA50B92CD8B66A3AD3F4F22C4FED
9BA44C2621385CB966EBA586F72C284D731FABEE
A27677289986DB50844682F8ACB77FC2E86E29AC
A9C5DF4D22E99998D9875A5110C01C5A2F6059E7
DCFD35E0BF8CA7344752DE8B6FB21E8933C60243
F3A04C595DB5B6A5F1ECA43E3B7BBB100D811BBE
F7DA48BB64BCB84ECBA7EE6935CD23C10D498E23  
RUN set -ex; \  
for key in $GPG_KEYS; do \  
gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key" || \  
gpg --keyserver keyserver.pgp.com --recv-keys "$key" || \  
gpg --keyserver pgp.mit.edu --recv-keys "$key" ; \  
done  
  
ENV TOMCAT_MAJOR 8  
ENV TOMCAT_VERSION 8.5.23  
ENV TOMCAT_TGZ_URL
https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-
tomcat-$TOMCAT_VERSION.tar.gz  
# not all the mirrors actually carry the .asc files :'(  
ENV TOMCAT_ASC_URL
https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-
tomcat-$TOMCAT_VERSION.tar.gz.asc  
  
RUN set -x \  
\  
&& apk add --no-cache --virtual .fetch-deps \  
ca-certificates \  
tar \  
openssl \  
&& wget -O tomcat.tar.gz "$TOMCAT_TGZ_URL" \  
&& wget -O tomcat.tar.gz.asc "$TOMCAT_ASC_URL" \  
&& gpg --batch --verify tomcat.tar.gz.asc tomcat.tar.gz \  
&& tar -xvf tomcat.tar.gz --strip-components=1 \  
&& rm bin/*.bat \  
&& rm tomcat.tar.gz* \  
\  
&& nativeBuildDir="$(mktemp -d)" \  
&& tar -xvf bin/tomcat-native.tar.gz -C "$nativeBuildDir" \--strip-
components=1 \  
&& apk add --no-cache --virtual .native-build-deps \  
apr-dev \  
coreutils \  
dpkg-dev dpkg \  
gcc \  
libc-dev \  
make \  
"openjdk${JAVA_VERSION%%[-~bu]*}"="$JAVA_ALPINE_VERSION" \  
openssl-dev \  
&& ( \  
export CATALINA_HOME="$PWD" \  
&& cd "$nativeBuildDir/native" \  
&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \  
&& ./configure \  
\--build="$gnuArch" \  
\--libdir="$TOMCAT_NATIVE_LIBDIR" \  
\--prefix="$CATALINA_HOME" \  
\--with-apr="$(which apr-1-config)" \  
\--with-java-home="$(docker-java-home)" \  
\--with-ssl=yes \  
&& make -j "$(nproc)" \  
&& make install \  
) \  
&& runDeps="$( \  
scanelf --needed --nobanner --recursive "$TOMCAT_NATIVE_LIBDIR" \  
| awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \  
| sort -u \  
| xargs -r apk info --installed \  
| sort -u \  
)" \  
&& apk add --virtual .tomcat-native-rundeps $runDeps \  
&& apk del .fetch-deps .native-build-deps \  
&& rm -rf "$nativeBuildDir" \  
&& rm bin/tomcat-native.tar.gz  
  
# verify Tomcat Native is working properly  
RUN set -e \  
&& nativeLines="$(catalina.sh configtest 2>&1)" \  
&& nativeLines="$(echo "$nativeLines" | grep 'Apache Tomcat Native')" \  
&& nativeLines="$(echo "$nativeLines" | sort -u)" \  
&& if ! echo "$nativeLines" | grep 'INFO: Loaded APR based Apache Tomcat
Native library' >&2; then \  
echo >&2 "$nativeLines"; \  
exit 1; \  
fi  
  
# Create dirs if they don't exist yet  
RUN echo ${INSTALL_DASHBOARD_PATH}/daobs-data-dashboard && mkdir -p
${INSTALL_DASHBOARD_PATH} && mkdir -p ${INSTALL_DASHBOARD_PATH}/daobs-data-
dashboard  
RUN echo ${INSTALL_ETF_PATH} && mkdir -p ${INSTALL_ETF_PATH}  
  
# Adding the DAOS src  
ADD ./ ${CATALINA_HOME}/daobs  
  
WORKDIR ${CATALINA_HOME}/daobs  
  
RUN mvn install \  
-DskipTests -Drelax \  
-gs /usr/share/maven/ref/settings-docker.xml \  
-Pdocker \  
-Ddata.dir=${INSTALL_DASHBOARD_PATH}/daobs-data-dashboard \  
-Detf.installation.path=${INSTALL_ETF_PATH}  
  
# Build and install ETF  
WORKDIR ${CATALINA_HOME}/daobs/tasks/etf-validation-checker  
RUN mvn install -Drelax -DskipTests -gs /usr/share/maven/ref/settings-
docker.xml -Petf-download  
RUN mv ./ETF/ETF/* ${INSTALL_ETF_PATH}/.  
  
RUN cp ${CATALINA_HOME}/daobs/web/target/daobs.war ${CATALINA_HOME}/webapps  
#RUN cp -r /usr/local/tomcat/daobs/web/target/daobs/WEB-INF/datadir/
${INSTALL_DASHBOARD_PATH}/daobs-data-dashboard  
# Load kibana dashboards  
RUN npm install elasticdump -g  
  
# Cleanup  
RUN rm -rf ${CATALINA_HOME}/tomcat/daobs/  
RUN rm -rf /root/.m2/repos  
  
COPY ./wait-for-it.sh /wait-for-it.sh  
RUN chmod +x /wait-for-it.sh  
  
COPY ./docker-entry.sh /docker-entry.sh  
RUN chmod +x /docker-entry.sh  
  
EXPOSE 8080  
WORKDIR $CATALINA_HOME  
#CMD ["catalina.sh", "run"]  

