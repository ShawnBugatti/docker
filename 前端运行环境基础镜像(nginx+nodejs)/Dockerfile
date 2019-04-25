#依赖docker官方nginx镜像，系统为debian
FROM nginx

#nodejs建议使用py2.6/2.7版本否则安装会报错
ADD Python-2.7.16.tgz /usr/local/

#源码方式编译安装python及相关运行环境
RUN  cd /usr/local/Python-2.7.16 \
    && ls -al \
    && apt-get update \
    && apt-get -yqq install make \
    && apt-get -yqq install gcc \
    && apt-get -yqq install g++ \
    && apt-get -yqq install ruby zlib1g zlib1g.dev \
    && apt-get -yqq install libffi-dev \
    && ./configure --prefix=/opt/python2.7.16 \
    && make \
    && make install \
    && ln -s /opt/python2.7.16/bin/python2.7 /usr/bin/python \
    && python --version

ADD node-v10.15.3.tar.gz /usr/local/

#源码方式编译安装nodejs
RUN cd /usr/local/node-v10.15.3 \
    && ls -al \
    && ./configure --prefix=/opt/nodejs10.15.3 \
    && make && make install \
    && ln -s /opt/nodejs10.15.3/bin/node /usr/bin/node \
    && ln -s /opt/nodejs10.15.3/bin/npm /usr/bin/npm \
    && node -v
