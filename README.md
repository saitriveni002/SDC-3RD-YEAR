


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
nginx-tomcat/
│
├── docker-compose.yml
│
├── nginx/
│   └── default.conf
│
└── webapp/
    └── index.html
server {

    listen 80;

    location / {

        proxy_pass http://tomcat:8080;

        proxy_set_header Host $host;

        proxy_set_header X-Real-IP $remote_addr;

        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    }

}
services:

  db:
    image: mysql:8.0
    container_name: mysql-db
    restart: always

    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wpuser
      MYSQL_PASSWORD: wp123

    volumes:
      - db-data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    restart: always

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wpuser
      WORDPRESS_DB_PASSWORD: wp123
      WORDPRESS_DB_NAME: wordpress

    depends_on:
      - db

    volumes:
      - wp-data:/var/www/html

volumes:
  db-data:
  wp-data:
////
services:

  tomcat:
    image: tomcat:9.0
    container_name: tomcat-server
    restart: always

    volumes:
      - ./webapp:/usr/local/tomcat/webapps/ROOT

    networks:
      - app-network

  nginx:
    image: nginx:latest
    container_name: nginx-server
    restart: always

    ports:
      - "8081:80"

    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro

    depends_on:
      - tomcat

    networks:
      - app-network

networks:
  app-network:
    driver: bridge
| Plugin | Purpose |
|---|---|
| Git | Connects Jenkins to GitHub repositories |
| Pipeline | Creates pipeline projects |
| Git Client | Supports Git operations |
| Maven Integration | Provides Maven-related integration |


node {

    try {

        stage('Checkout') {

            echo 'Fetching source code from GitHub'

            git branch: 'main',
                url: 'GITHUB_REPOSITORY_URL'

        }

        stage('Build') {

            echo 'Building the Java application'

            bat 'mvn clean compile'

        }

        stage('Test') {

            echo 'Running test cases'

            bat 'mvn test'

        }

        stage('Package') {

            echo 'Packaging the application'

            bat 'mvn package'

        }

        stage('Success') {

            echo 'BUILD SUCCESSFUL'

        }

    }

    catch (Exception e) {

        echo 'BUILD FAILED'

        throw e

    }

}

pipeline {
    agent any

    tools {
        maven 'maven-home'
    }

    stages {
        stage('Git Repo and Clean') {
            steps {
                bat 'rmdir /s /q sample-maven-java-project'
                bat 'git clone https://github.com/USERNAME/sample-maven-java-project.git'
                bat 'mvn clean -f sample-maven-java-project/pom.xml'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install -f sample-maven-java-project/pom.xml'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test -f sample-maven-java-project/pom.xml'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -f sample-maven-java-project/pom.xml'
            }
        }
    }
}
