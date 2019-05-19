FROM zx1263526/zx-repo:centos-7.5.1804

RUN cd /tmp \
    && curl -L -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -k "http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jdk-8u45-linux-x64.rpm" \
    && yum localinstall -y jdk-8u45-linux-x64.rpm \
    rm -rf jdk-8u45-linux-x64.rpm

ENV JAVA_HOME /usr/java/default

ENV PATH ${PATH}:${JAVA_HOME}/bin