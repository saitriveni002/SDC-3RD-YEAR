# SDC-3RD-YEAR
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.aiolms</groupId>
    <artifactId>AI-OLMS</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!-- Web application -->
    <packaging>war</packaging>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <maven.compiler.release>17</maven.compiler.release>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <build>
        <finalName>AI-OLMS</finalName>

        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.14.1</version>
                <configuration>
                    <release>17</release>
                </configuration>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.4.0</version>
            </plugin>
        </plugins>
    </build>

</project>
//java project 
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
            http://maven.apache.org/POM/4.0.0
            https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.aiolms</groupId>
    <artifactId>AI-OLMS</artifactId>
    <version>1.0-SNAPSHOT</version>

    <packaging>war</packaging>

    <name>AI-OLMS</name>
    <description>AI Online Learning Management System</description>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

        <java.version>17</java.version>
        <maven.compiler.release>17</maven.compiler.release>

        <servlet.api.version>6.1.0</servlet.api.version>
    </properties>

    <dependencies>

        <!-- Jakarta Servlet API -->
        <!-- Provided by the application server such as Tomcat -->
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>${servlet.api.version}</version>
            <scope>provided</scope>
        </dependency>

    </dependencies>

    <build>

        <finalName>AI-OLMS</finalName>

        <plugins>

            <!-- Java Compiler -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.14.1</version>
                <configuration>
                    <release>${java.version}</release>
                </configuration>
            </plugin>

            <!-- WAR packaging -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.4.0</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>

            <!-- Unit testing -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.5.3</version>
            </plugin>

        </plugins>

    </build>

</project>
Solve this model paper as a **hands-on lab guide**.

For each question, tell me:

1. **Where to execute** (Git Bash / CMD / Eclipse / Docker).
2. **Exact command/code to type**.
3. **Step-by-step execution procedure**.
4. **Expected output/result**.
5. **How to verify it worked**.
6. **What to do if an error occurs**.

Keep explanations short and simple. Give commands that I can **copy-paste and execute directly**. For Maven, Git, GitHub, Docker, and Tomcat, show the complete practical workflow from start to finish.

Do not give only theory—teach me **what to type, where to type it, and what should happen**.
//java
FROM openjdk:17-jdk-alpine
WORKDIR /app
COPY target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]

//wed

FROM tomcat:10-jdk17
RUN rm -rf /usr/local/tomcat/webapps/*
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
If you mean **how to run a Docker Hub image**, the basic flow is:

```
# 1. Install Docker
# Then verify
docker --version

# 2. Login to Docker Hub
docker login

# 3. Pull an image
docker pull nginx

# 4. Run the container
docker run -d -p 8080:80 --name my-nginx nginx

# 5. Check running containers
docker ps

# 6. Stop it
docker stop my-nginx

# 7. Remove it
docker rm my-nginx
```

 ### If you have your own image on Docker Hub

 For an image like `username/myapp:latest`:

```
docker login
docker pull username/myapp:latest
docker run -d -p 8080:8080 --name myapp username/myapp:latest
```

 ### Flow for pushing your own image

```
# Build
docker build -t username/myapp:latest .

# Login
docker login

# Push to Docker Hub
docker push username/myapp:latest
```

 So the overall flow is:

 **Dockerfile → `docker build` → Docker image → `docker push` → Docker Hub → `docker pull` → `docker run`**

 If you tell me whether you're trying to **run an existing Docker Hub image** or **create/push your own image**, I can give you the exact step-by-step flow.
