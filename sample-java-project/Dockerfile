# Stage 1: Build
FROM ubuntu AS builder
WORKDIR /app

RUN apt update -y && \
    apt install -y git maven openjdk-17-jdk

# Clone the repository and build the application
RUN git clone https://github.com/srikanthv247/sample-java-project.git
WORKDIR /app/sample-java-project
RUN mvn package

# Stage 2: Deploy
FROM tomcat:9-jdk17
COPY --from=builder /app/sample-java-project/target/*.war /usr/local/tomcat/webapps/
RUN chmod 755 /usr/local/tomcat/webapps/*.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
