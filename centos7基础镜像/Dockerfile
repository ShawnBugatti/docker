FROM centos:7.5.1804

#Import the Repositories
RUN rm -rf /etc/yum.repos.d/*
ADD etc/yum.repos.d/CentOS7-Base-163.repo /etc/yum.repos.d/
ADD etc/yum.repos.d/Aliyun-Centos-7.repo /etc/yum.repos.d/

#Base Install
RUN rpm --rebuilddb \
    && yum -y install \
        vim \
        tar \
        net-tools \
        xz \
        python-setuptools \
        yum-versionlock \
        telnet \
        zip \
        unzip \
        net-tools \
    && yum versionlock add \
        vim \
        xz \
        tar \
        python-setuptools \
        yum-plugins-versionlock \
    && rm -rf /var/cache/yum/* \
    && yum clean all

#Install supervisord(required to run more than a single process in a container)
#Note: EPEL package lacks /usr/bin/pidproxy
#We require supervisor-stdout to allow output of services started by
#supervisord to be easily inspected with "docker logs".

RUN easy_install \
        'supervisor == 3.3.1' \
        'supervisor-stdout == 0.1.1' \
     && mkdir -p \
        /var/log/supervisor/

#CTC Timezone & Networking
RUN ln -sf \
        /usr/share/zoneinfo/Asia/Shanghai \
        /etc/localtime \
    && echo "NETWORKING=yes" > /etc/sysconfig/network

RUN mkdir -p \
        /etc/supervisord.d/

ADD etc/service-config/supervisor/supervisord.conf /etc/

#Purge

RUN rm -rf /etc/ld.so.cache \
    ; rm -rf /sbin/sln \
    ; rm -rf /usr/{{lib,share}/locale,share/{man,doc,info,cracklib,i18n},{lib,lib64}/gconv,bin/localedef,sbin/build-locale-archive} \
    ; rm -rf /{root,tmp,var/cache/{ldconfig,yum}}/* \
    ; > /etc/sysconfig/i18n

# Ulimit
RUN echo "* soft nofile 655350" >> /etc/security/limits.conf & \
    echo "* hard nofile 655350" >> /etc/security/limits.conf & \
    echo "@root soft nproc 655350" >> /etc/security/limits.conf & \
    echo "@root hard nproc 655350" >> /etc/security/limits.conf & \
    echo "ulimit -SH 655350" >> /etc/rc.local

# Set default environment variables
#Set image metadata
ARG RELEASE_VERSION="1.0.0"
LABEL \
        description="CentOS-7 7.5.1804 x86_64 - Supervisor /" \
        vendor="CentOS"

CMD ["/usr/bin/supervisord","--configuration=/etc/suprtvisord.conf"]
