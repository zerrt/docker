#SETUP JREBEL
FROM alpine as jrebel
WORKDIR /tmp
USER root
RUN apk update && apk add curl
RUN curl -O http://dl.zeroturnaround.com/jrebel-stable-nosetup.zip
RUN unzip jrebel-stable-nosetup.zip

#APP BUILD
#FROM gradle:4.3.1-jdk8 AS app-build
#ENV version=11.3.1
#COPY --chown=gradle:gradle . /home/gradle/src
#RUN chmod -R 777 /home/gradle/src
#WORKDIR /home/gradle/src
#RUN ./gradlew --no-daemon war
#RUN cp  web/build/libs/web.war /tmp/app


#WAS SERVER
FROM ibmcom/websphere-traditional:9.0.5.2-ubi

#SETUP LOGGING
ENV ENABLE_BASIC_LOGGING=true
RUN /work/configure.sh

#SETUP JVM
COPY --from=jrebel /tmp/jrebel /tmp/jrebel
RUN wsadmin.sh -lang jython -conntype NONE -c "AdminConfig.modify(AdminConfig.list('JavaVirtualMachine', AdminConfig.list('Server')), [['genericJvmArguments', '-Xshareclasses:none -agentpath:/tmp/jrebel/lib/libjrebel64.so -Drebel.remoting_plugin=true']])"

#SETUP DATASOURCES

#DEPLOY APP
#COPY --from=app-build /home/gradle/src/web/build/libs/web.war /tmp/app/web.war
#RUN wsadmin.sh -lang jython -conntype NONE -c "AdminApp.install('/tmp/app/web.war', '[ -appname web -contextroot /web -MapWebModToVH [[ web.war web.war,WEB-INF/web.xml default_host]]]')"
#REMOVE tmp war 
#USER root
#RUN rm /tmp/app/web.war



#LABELS
LABEL maintainer="tyler.zerr@sasktel.com"
LABEL org.label-schema.version="1.0-alpha"
LABEL org.label-schema.docker.cmd="docker run -d -p 9043:9043 -p 9443:9443 -p 2809:2809 -p 8880:8880 -p 9633:9633 -p 7777:7777 -v ~/.jrebel:/home/was/.jrebel  ./logs:/logs was-demo"
LABEL org.label-schema.debug="docker run --tty -i $CONTAINER /bin/bash"






#docker build -t was-demo .
#docker run -d -p 9043:9043 -p 9443:9443 -p 2809:2809 -p 8880:8880 -p 9633:9633 -p 7777:7777 -v ~/.jrebel:/home/was/.jrebel  ./logs:/logs was-demo