FROM openjdk:8-jre-alpine
ARG WORKSPACE
RUN mkdir /app

RUN echo **********************
RUN echo hostname
RUN echo **********************

RUN echo $WORKSPACE
#RUN ls $WORKSPACE

RUN echo **********************
RUN ls /var/jenkins_home/workspace/maven-pipeline

#COPY "${WORKSPACE}"/targer/*.jar /app/app.jar

#CMD java -jar /app/app.jar
