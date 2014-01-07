FROM paas/base

# 1. Packages / Dependencies

RUN wget -q -O - http://nginx.org/keys/nginx_signing.key | apt-key add - && \
 echo "deb http://nginx.org/packages/ubuntu/ precise nginx" >> /etc/apt/sources.list && \
 apt-get update && \
 apt-get -y install nginx

# 2. nginx

ADD nginx.conf /etc/nginx/
ADD default.conf /etc/nginx/conf.d/

# 3. collectd

ADD nginx.collectd.conf /opt/collectd/etc/conf.d/

# Startup

ADD nginx.supervisord.conf /etc/supervisor/conf.d/
