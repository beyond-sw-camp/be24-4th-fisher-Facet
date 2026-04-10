# 빌드 단계
FROM gradle:8.14.4-jdk17 AS builder
WORKDIR /app

COPY keystore.p12        ./
COPY build.gradle        ./
COPY settings.gradle     ./

RUN gradle dependencies --no-daemon

COPY ../src  ./src
RUN gradle bootjar --no-daemon

# 실행 단계
FROM openjdk:17-ea-17-slim
COPY   --from=builder  /app/build/libs/*.jar   /app.jar
COPY   --from=builder  /app/keystore.p12   /keystore.p12
EXPOSE 8080
CMD ["java", "-jar", "/app.jar"]