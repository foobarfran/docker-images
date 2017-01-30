# Supported tags and respective ```Dockerfile``` links
 * ```8-1.0.0```, ```latest``` [8-1.0.0/Dockerfile](https://github.com/francomorinigo/docker-images/tree/master/java-web-app/8-1.0.0)

### Features
 - Lightweight base image for self contained java web apps
 - Multi environment support
 - NewRelic support
 - Tunning JVM by environment
 - Enable JMX by environment
 - Enable debugging by environment

# Project structure
```
.
+-- pom.xml
+-- src
|   +-- ...
+-- conf
|   +-- common
|   |   +-- fooCommon.properties
|   +-- development
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- staging
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- production
|   |   +-- logback.xml
|   |   +-- deploy-propeties.json
|   +-- newrelic
|   |   +-- newrelic.yml
```

&nbsp;
### Put the deploy-properties.json file in each env directory

```json

{
	"jvmArguments":"-Xms1024m -Xmx1024m",
	"debugEnabled": false,
	"jmxEnabled": true,
	"newRelicEnabled": true,
	"mainClass": "com.foo.App"
}
```

&nbsp;
### Used ports
 - 8080 for webApp
 - 9010 for debugging or jmx connections

# Use the base image

```docker
FROM francomorinigo/java-web-app:8-1.0.0

ARG version

# Uncomment if you use newrelic
# COPY target/newrelic/newrelic.jar application/newrelic/newrelic.jar
COPY conf application/
COPY target/fooApp-$version.jar application/fooApp-$version.jar

```
&nbsp;
```dockerfile
docker build -t fooApp:fooVersion . --build-arg version=fooVersion
```

&nbsp;
# Run a container

 ```bash
 $ docker run -e ENV=development -e HOST_IP=fooIp -v /application --name fooApp -P  fooApp
 ```
