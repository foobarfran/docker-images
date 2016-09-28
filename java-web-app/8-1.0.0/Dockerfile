FROM openjdk:8-jre-alpine
MAINTAINER Franco Morinigo <franco.m87@gmail.com>

# Install jq
RUN apk update \
 && apk add jq \
 && rm -rf /var/cache/apk/*

# Copy java startup script
COPY start.sh start.sh

CMD ["./start.sh"]

# Application port
EXPOSE 8080

# JMX or Debugging port
EXPOSE 9010
