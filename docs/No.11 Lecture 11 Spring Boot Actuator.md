## Spring Boot Actuator

Problems in the real situation:

- How can I monitor and manage my application ?

- How can I check the application health ?

- How can I access application metrics ?

So the solution is using the `Spring Boot Actuator`, exposes endpoints to monitor and manage your application. You easily get DevOps functionally out-of-the-box. 

It simply add the dependency to your POM files. REST endpoints are automatically added to your application.

### 1. Add the Spring Boot Actuator into Project

Adding the dependency to your POM Files to add the Maven Project new Library

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

It automatically exposes endpoints for metrics out-of-the-box. Endpoints are prefixed with **`/actuator`**

| Name    | Description                                      |
|---------|--------------------------------------------------|
| /health | Health information about your application      . |
| ...     |                                                  |

### 2. Health Endpoints in Spring Project

`/health` it is support by the Spring Actuator to check the status of your application in Spring Boot Project.

It normally used by monitoring apps to see if your app is `up` or `down`, So if you want to see this status of your Spring Boot Application go to the url **`domain/actuator/health`**.

For example if you run your application in the `localhost` with port `8080` you can go to the url `localhost::8080/actuator/health`.

It will display the status like the below Json

```json
{
  "status": "UP"
}
```

Health status is customizable based on your own bussiness logic.

### 3. Exposing Endpoints

By default, only `/health` is exposed, to expose all actuator endpoints over HTTP, go to the `/src/main/resources/application.properties` and add the code belows

```bash
# Use wildcard "*" to expose all endpoints
# Can also expose individual endpoints with a comma-delimited list
#
management.endpoints.web.exposure.include=*
```

The `/info` endpoints can provide information about your application.

To exposed the `/info`, go to the `/src/main/resources/application.properties` and add the code below. And the another endpoints will add and separate by the `,` like `health,info,...`

```java
management.endpoints.web.exposure.include=health,info
management.info.env.enabled=true
```


### 3. Info Endpoints

Now, look into the `info` endpoints, it gives information about your application, the default is empty

```json
{}
```

So you need update `application.properties` with your application info, go to the `/src/main/resources/application.properties` update some information like below

```java
info.app.name=My Spring Boot Project
info.app.description=A new Spring Boot Project
info.app.version=1.0.0
```

So now when go to `/actuator/info` you will see all thing you are setup

```json
{
  "app": {
    "name": "My Spring Boot Project",
    "description": "A new Spring Boot Project",
    "version": "1.0.0"
  }
}
```

There are 10+ Spring Boot Actuator Endpoints popular in the [Spring document](https://docs.spring.io/spring-boot/reference/actuator/endpoints.html#page-title)

| Name         | Description                                            |
|--------------|--------------------------------------------------------|
| /auditevents | Audit events for your application                      |
| /beans       | List of all beans registered in the Spring Application |
| /mappings    | List of all @RequestMapping paths                      |

### 4. Get a list of Beans

Access to the url `/actuator/beans`, if you use in the `localhost` with port `8080` you will access the url `http://localhost:8080/actuator/beans`.

You will see all the beans of the `spring` application you include in the `dependencies` in the `pom.xml`.

### 5. Development Process 

1. Edit `pom.xml` and add `spring-boot-starter-actuator`

2. View actuator endpoints for `/health`

3. Edit `application.properties` to customize `/info`

### 6. Spring Boot Actuator Security

You may not want to expose all of this information about your spring project. So you need add Spring Security to project and all endpoints are need to secured.

So go to the `pom.xml` add the dependency `spring-boot-starter-security` into the `dependencies`

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency
```

However, the endpoints `/heath` still available, you can disable it if you want. 

### 7. Endpoints Secured

Now when you access to the endpoints `/actuator/beans`, Spring Security will prompt you to the form to login page.

Now you need to know the name and password. With the username is default `user`, and you need to find the password in the console of running applications.

![alt text](/images/image-03.png)

### 8. Spring Security Configuration

You can override the default user name and generated password by go to the `/src/main/resources/application.properties` and add the code with the format

```xml
spring.security.user.name=<username>
spring.security.user.password=<password>
```

For example you can add modify the account for the admin like the code below

```xml
spring.security.user.name=admin
spring.security.user.password=admin
```

You can customize Spring Security for the Spring Boot Actuator by use the database for roles, encrypted, passwords, etc...

### 9. Excluding Endpoints

Sometimes you want to exclude some of endpoints like `/health`, or `/info` you need to config in the `/src/main/resources/application.properties` the code below

```xml
# Exclude individual endpoints with a comma-delimited list
#
management.endpoints.web.exposure.exclude = health, info
```

To learn more about the Endpoints, we can read it in the main documents of [Spring Actuator](https://docs.spring.io/spring-boot/reference/actuator/endpoints.html#page-title).









