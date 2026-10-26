FROM eclipse-temurin:8-jre-alpine

EXPOSE 8080

COPY ./build/libs/app.jar /usr/app/app.jar
WORKDIR /usr/app

CMD ["java", "-jar", "app.jar"]