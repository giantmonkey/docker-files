FROM ubuntu

# 0. random tools

RUN apt-get update && \
 apt-get -y install build-essential wget

# 1. supervisor

RUN apt-get -y install supervisor && \
 mkdir -p /var/log/supervisor

ADD supervisord.conf /etc/supervisor/conf.d/
ADD collectd.supervisord.conf /etc/supervisor/conf.d/

# 2. collectd

# dependencies for collectd plugins
RUN apt-get -y install libpq-dev libcurl4-openssl-dev libvarnishapi-dev libyajl-dev

ADD SHA512SUM /tmp/
RUN cd /tmp/ && \
 wget -q http://collectd.org/files/collectd-5.4.0.tar.bz2 && \
 cat collectd-5.4.0.tar.bz2 | sha512sum SHA512SUM && \
 tar xf collectd-5.4.0.tar.bz2

RUN cd /tmp/collectd-5.4.0 && \
 ./configure --disable-daemon && \
 make -j3 && \
 make install

RUN rm -rf /tmp/collectd-5.4.0

RUN mkdir -p /opt/collectd/etc/conf.d

ADD collectd.conf /opt/collectd/etc/
ADD supervisord.collectd.conf /opt/collectd/etc/conf.d/

ENTRYPOINT ["supervisord"]
