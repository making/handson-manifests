FROM maven as deps
RUN echo -e '<?xml version="1.0" encoding="UTF-8"?>\n\
<project xmlns="http://maven.apache.org/POM/4.0.0"\n\
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"\n\
     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">\n\
  <modelVersion>4.0.0</modelVersion>\n\
  <parent>\n\
    <groupId>org.springframework.boot</groupId>\n\
    <artifactId>spring-boot-starter-parent</artifactId>\n\
    <version>2.6.3</version>\n\
    <relativePath/>\n\
  </parent>\n\
  <groupId>com.example</groupId>\n\
  <artifactId>deps</artifactId>\n\
  <version>0.0.1-SNAPSHOT</version>\n\
  <name>deps</name>\n\
  <description>deps</description>\n\
  <properties>\n\
    <java.version>11</java.version>\n\
  </properties>\n\
  <dependencies>\n\
    <dependency>\n\
      <groupId>org.springframework.boot</groupId>\n\
      <artifactId>spring-boot-starter-data-mongodb</artifactId>\n\
    </dependency>\n\
    <dependency>\n\
      <groupId>org.springframework.integration</groupId>\n\
      <artifactId>spring-integration-mongodb</artifactId>\n\
    </dependency>\n\
  </dependencies>\n\
</project>'\
>> /tmp/pom.xml
RUN mvn -X -f /tmp/pom.xml dependency:copy-dependencies -DoutputDirectory=/libs

FROM springcloudstream/s3-source-kafka:3.2.0
COPY --from=deps /libs/*.jar /app/libs/
