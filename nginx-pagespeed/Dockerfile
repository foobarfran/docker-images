FROM ubuntu
MAINTAINER <franco.m87@gmail.com>

RUN apt-get update && apt-get install -y \
        wget \
        unzip \
        g++  \
        libpcre3 \
        libpcre3-dev \
        zlib1g-dev \
        build-essential

# Download ngx_pagespeed
ARG NPS_VERSION=1.12.34.2-beta

RUN wget https://github.com/pagespeed/ngx_pagespeed/archive/v${NPS_VERSION}.zip && \
    unzip v${NPS_VERSION}.zip

WORKDIR ngx_pagespeed-${NPS_VERSION}/

RUN psol_url=https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz && \
    [ -e scripts/format_binary_url.sh ] && psol_url=$(scripts/format_binary_url.sh PSOL_BINARY_URL) && \
    wget ${psol_url} && \
    tar -xzvf $(basename ${psol_url})

# Download and build nginx with support for pagespeed
ARG NGINX_VERSION=1.11.9

WORKDIR /

RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    tar -xvzf nginx-${NGINX_VERSION}.tar.gz

WORKDIR nginx-${NGINX_VERSION}/

RUN ./configure --add-module=/ngx_pagespeed-${NPS_VERSION} ${PS_NGX_EXTRA_FLAGS} && \
    make && \
    make install

# Run nginx
EXPOSE 80 443
CMD ["objs/nginx", "-g", "daemon off;"]
