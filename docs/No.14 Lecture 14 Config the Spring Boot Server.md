## Configuring the Spring Boot Server

Spring Boot can be configured in the `application.properties` file, like a server port, context path, actuator, security and ... Spring Boot has 1000+ properties... wowzers!

You can see all of list of common properties in the [Spring Boot Common Application Properties](https://docs.spring.io/spring-boot/appendix/application-properties/index.html)

The properties are roughly grouped into the following category

- Core
- Web
- Security
- Data
- Actuator
- Integration
- DevTools
- Testing

### 1. Core Properties

Go to the location of this file `/src/main/resources/application.properties` and modify the file by the code below

```java
# Log level severity mapping
logging.level.org.springframework=DEBUG
logging.level.org.hibernate=TRACE
logging.level.com.tbin=INFO
```

We are set **logging levels** based on the package names. Here is some of logging levels:

- TRACE
- DEBUG
- INFO
- WARN
- ERROR
- FATAL
- OFF

You also can write a log into the **determine location** file like the code below
with the `...` is the location to the file of log you want to store in.

```xml
# Log file name
logging.file.name=my-spring-boot-apps.log
logging.file.path="..."
```

You can read more in the [Spring Boot Logging](https://docs.spring.io/spring-boot/reference/features/logging.html)

### 2. Web Properties

Now we also go to the `/src/main/resources/application.properties` and change some of properties use for website development.

First change the HTTP Server Port. The default port is 8080 

```xml
# HTTP Server Port
server.port = ...
```

Now we also can change the context path of the application. By the default, the context path is `/`

```xml
sever.servlet.context-path=/spring-boot
```

So it mean all requests should be prefixed with `/spring-boot`. Now when we need access to the url path of the website `http://localhost:8080/spring-boot`

We also can set the default HTTP Session Time Out of the Spring Boot application. In the code below the `...` is the number of `minutes` you set for the time out of the HTTP Session. The default Session Time Out is 30 minutes.

```xml
server.servlet.session.timeout=...m
```

### 3. Actuator Properties

Now we also go to the `/src/main/resources/application.properties` and change some of properties use for actuator properties, like the `endpoints`. The default of Base path for actuator endpoints is also `/actuator`.

```xml
# Endpoints to include by name or willcard
management.endpoints.web.exposure.include=*

# Endpoints to exclude by name or willcard
management.endpoints.web.exposure.exclude=beans,mapping

# Base path for actuator endpoints
management.endpoints.web.base-path=/actuator
```

### 4. Security Properties

Now we also go to the `/src/main/resources/application.properties` and change some of properties use for security properties, like the `username`, or `password`. 

```xml
# Configure Your Spring Security Account
#
spring.security.user.name=admin
spring.security.user.password=admin
```

However, we can customize Spring Security for Spring Boot Actuator by many method like use the database for roles, encrypted password, etc...

### 4. Data Properties

Now we also go to the `/src/main/resources/application.properties` and change some of properties use for data properties.

```xml
# JDBC URL For the Database
spring.datasource.url=jdbc::mysql://localhost:3306/..

# Login username of the databse
spring.datasource.username=admin

# Login password of the databse
spring.datasource.password=admin
```