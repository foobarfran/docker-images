# Supported tags and respective ```Dockerfile``` links
 * ```latest``` [latest/Dockerfile](https://github.com/francomorinigo/docker-images/tree/master/nginx-pagespeed)

### About this image
This image was built acording to the [pagespeed build documentation](https://modpagespeed.com/doc/build_ngx_pagespeed_from_source).

### Configuration
    FROM francomorinigo/nginx-pagespeed
    COPY nginx.conf /usr/local/nginx/conf/nginx.conf

### Run a container
    docker run -P francomorinigo/nginx-pagespeed

### Build with specific versions
    docker build --build-arg NGINX_VERSION=1.11.9 --build-arg NPS_VERSION=1.12.34.2-beta -t nginx-pagespeed .
