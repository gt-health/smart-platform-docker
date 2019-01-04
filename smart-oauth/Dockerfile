FROM openjdk:alpine
RUN apk update
RUN apk add bash
ADD hspc-reference-auth-server-webapp-*.war app.war
ADD jetty-runner.jar jetty-runner.jar
ADD jetty.xml jetty.xml

# Add auth.properites file and replace the auth.properites in the app.war file
RUN mkdir -p WEB-INF/classes/config
COPY auth.properties WEB-INF/classes/config/auth.properties
#ADD WEB-INF/classes/config/auth.properties WEB-INF/classes/config/auth.properties
RUN jar uvf app.war WEB-INF/classes/config/auth.properties

ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Dspring.profiles.active=local,users-local -jar jetty-runner.jar --config jetty.xml --path /smart-oauth app.war" ]
