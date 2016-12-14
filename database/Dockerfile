FROM centos:centos6.7
MAINTAINER Kyawphyonaing

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y wget tar make gcc

# install redis
RUN cd /tmp && \
      wget http://download.redis.io/redis-stable.tar.gz && \
      tar xvzf redis-stable.tar.gz && \
      cd redis-stable && \
      make && \
      make install && \
      cp -f src/redis-sentinel /usr/local/bin && \
      mkdir -p /etc/redis && \
      cp -f *.conf /etc/redis

RUN sed -e "s/# bind 127.0.0.1/bind 0.0.0.0/" -i /etc/redis/redis.conf

# install mysql
RUN cd /tmp && \
      wget http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-5.5.46-1.el6.x86_64.rpm-bundle.tar && \
      tar xvf MySQL-5.5.46-1.el6.x86_64.rpm-bundle.tar && \
      yum localinstall -y MySQL-shared-compat-5.5.46-1.el6.x86_64.rpm && \
      yum localinstall -y MySQL-shared-5.5.46-1.el6.x86_64.rpm && \
      yum localinstall -y MySQL-server-5.5.46-1.el6.x86_64.rpm && \
      yum localinstall -y MySQL-client-5.5.46-1.el6.x86_64.rpm && \
      yum localinstall -y MySQL-devel-5.5.46-1.el6.x86_64.rpm

#Remove zips
RUN cd / && rm -rf /tmp/*

EXPOSE 6379 3306
CMD ["redis-server", "/etc/redis/redis.conf"]
