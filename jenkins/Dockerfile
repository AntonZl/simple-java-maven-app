FROM openjdk:8-jre-alpine
ARG WORKSPACE
RUN mkdir /app


RUN echo "Hostname: $(hostname)"


RUN echo "This is the WORKSPACE path: $WORKSPACE"
RUN ls $WORKSPACE/target

#COPY "${WORKSPACE}"/targer/*.jar /app/app.jar

#CMD java -jar /app/app.jar
