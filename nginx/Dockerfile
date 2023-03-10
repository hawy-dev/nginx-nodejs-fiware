ARG NGINX_VERSION=1.23.3

FROM nginx:$NGINX_VERSION

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       wget \
       build-essential \
       libpcre3 \
       libpcre3-dev \
       zlib1g \
       zlib1g-dev \
       libssl-dev \
       git

RUN wget https://nginx.org/download/nginx-$NGINX_VERSION.tar.gz \
    && tar -xzf nginx-$NGINX_VERSION.tar.gz \
    && cd nginx-$NGINX_VERSION \
    && git clone https://github.com/openresty/headers-more-nginx-module.git

RUN cd nginx-$NGINX_VERSION \
    && ./configure --with-compat --add-dynamic-module=headers-more-nginx-module \
    && make modules

RUN cp /nginx-$NGINX_VERSION/objs/*.so /usr/lib/nginx/modules/

RUN sed -i 's/#gzip_/gzip_/g' /etc/nginx/nginx.conf
RUN sed -i 's/#more_set_headers/more_set_headers/g' /etc/nginx/nginx.conf