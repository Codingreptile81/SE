# Software Engineering Lab Exam - Full Guide

This README provides a step-by-step guide with answers and commands to answer **Lab Internal I - Set 2** questions on **SRS, Maven, Git, and Docker**.

---

## QI. Software Requirement Specification (SRS)

**Abstract**  
The Modular Java Project (MJP) is an online event management system designed to simplify the organization and participation of events. It enables users to view upcoming events, register/login securely, book seats, and receive confirmation emails. The system includes modules for event listing, authentication, booking and payment, notifications, and admin management, ensuring scalability and maintainability.

**Functional Requirements**
1. User registration and login  
2. Event listing and search  
3. Seat booking and confirmation  
4. Email notification for registration/booking  
5. Admin module for adding/updating events  

**Non-Functional Requirements**
1. Performance: System should respond within 2 seconds for booking operations.  
2. Reliability/Error Handling: Handle invalid inputs gracefully with error messages.  
3. Maintainability: Code must follow modular architecture for easy updates.  

**User Roles**
- **Admin:** Add, update, or delete events; manage bookings.  
- **Registered User:** Register/login, book seats, view booking history.  
- **Guest:** View upcoming events, register for account.  

---
# Software Engineering Lab Exam - Docker & Maven Guide

This README provides a step-by-step guide with commands to answer **Lab Internal I - Set 2** questions on **Maven, Git, and Docker**.

---

## QIV. Docker Containerization

### 1. Dockerfile
```dockerfile
FROM openjdk:17
WORKDIR /app
COPY target/mjp.jar mjp.jar
CMD ["java", "-jar", "mjp.jar"]
```

### 2. Build Docker Image
```bash
docker build -t mjp-app .
```

### 3. List Images
```bash
docker images
```

### 4. Run a Container
```bash
docker run --name mjp-container mjp-app
```
Run in background:
```bash
docker run -d --name mjp-container mjp-app
```

### 5. View Containers
```bash
docker ps -a
```

### 6. Stop Container
```bash
docker stop mjp-container
```

### 7. Remove Container
```bash
docker rm mjp-container
```

### 8. Pull Redis Image
```bash
docker pull redis
```

### 9. Run Redis Container
```bash
docker run -d --name redis-server redis
```

### 10. Remove Docker Image
```bash
docker rmi mjp-app
```

---

## QV. Docker Compose

### docker-compose.yml
```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mjpdb
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

### Docker Compose Commands

- **Bring up services:**
```bash
docker compose up -d
```

- **View logs of app service:**
```bash
docker compose logs app
```

---

## Useful Git Commands (QIII)

- Initialize repo:
```bash
git init
git remote add origin <repo_url>
git branch -M main
git push -u origin main
```

- Fix last commit message (before push):
```bash
git commit --amend -m "Correct message"
```

- Use `.gitignore`:
```
/target/
```

- View commit history:
```bash
git log --oneline
```

- Stash changes and restore:
```bash
git stash
git checkout other-branch
git stash pop
```

- Create & merge feature branch:
```bash
git checkout -b gaming
touch file1 file2
git add .
git commit -m "Added gaming feature files"
git checkout main
git merge gaming
```

- Show last commit diff:
```bash
git show
```

- Difference between fetch & pull:
```bash
git fetch
git pull
```

- Unstage file:
```bash
git reset HEAD Calculator.java
```

- Modify last commit message:
```bash
git commit --amend -m "Updated message"
```

---

## Maven Commands (QII)

- Clone and build project:
```bash
git clone https://github.com/savram674/MJP.git
cd MJP
mvn clean install
```

- Add MySQL dependency (pom.xml):
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.0.33</version>
</dependency>
```

- Surefire plugin:
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-surefire-plugin</artifactId>
  <version>3.0.0</version>
</plugin>
```

- Create executable JAR (shade plugin):
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-shade-plugin</artifactId>
  <version>3.3.0</version>
  <executions>
    <execution>
      <phase>package</phase>
      <goals><goal>shade</goal></goals>
      <configuration>
        <transformers>
          <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
            <mainClass>com.example.Main</mainClass>
          </transformer>
        </transformers>
      </configuration>
    </execution>
  </executions>
</plugin>
```

---

This file covers **all key commands** needed for answering the lab exam questions.
