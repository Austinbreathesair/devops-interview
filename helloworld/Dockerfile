FROM gradle:7.4.0-jdk17 AS build

COPY build.gradle .

COPY settings.gradle .

COPY src ./src

RUN gradle clean build -x test

FROM openjdk:17-jdk-alpine

LABEL maintainer="austinbreathesair@gmail.com"

VOLUME /tmp

EXPOSE 8080

# STEP 1: Add the executable jar file in this container
RUN mkdir -p ./build/libs/

COPY build ./build

RUN ls ./build/

COPY ./build/libs/helloworld.jar ./build/libs/helloworld.jar

# STEP 2: Run the application when the container starts

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","./build/libs/helloworld.jar"]