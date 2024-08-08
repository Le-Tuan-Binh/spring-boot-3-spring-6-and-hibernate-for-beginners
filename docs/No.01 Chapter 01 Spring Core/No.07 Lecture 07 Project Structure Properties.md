## Project Structure Properties

### 1. Maven POM Files

`pom.xml` includes information that you give entered into Spring Initializr website when you create the new Spring project.

### 2. Application Properties

By default, Spring Boot will load properties from: **application.properties**

By default, it files is empty, you can add some `Spring Boot Properties` 

```bash
server.port=8585
```

Not only the properties of Spring Boot Application, you can add your `own custom properties` 

```bash
user.name=Le Tuan Binh
```

Get the value from the `application.properties` in the src example

For example we have file `application.properties` like below

```properties
spring.application.name=spring-boot-v1

# Configure Server Port
server.port=8484

# Configure Your Own Props
user.name=Le Tuan Binh
user.password=ltbinh
```

We can use those value in the class or somewhere in the project src like below, however this code below just one of the many way to use the value in `application.properties` we can have more way to use:

> **`Using @Value Annotation`**

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class SpringRestController {

    @Value("${user.name}")
    private String username;

    @Value("${user.password}")
    private String password;

    public void printAccount() {
        System.out.println("Username: " + username);
        System.out.println("Password: " + password);
    }
}
```


> **`Using Environment Object`**


```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.core.env.Environment;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class SpringRestController {

    private final Environment environment;

    @Autowired
    public SpringRestController(Environment environment) {
        this.environment = environment;
    }

    public void printAccount() {
        String username = environment.getProperty("user.name");
        String password = environment.getProperty("user.password");

        System.out.println("Username: " + username);
        System.out.println("Password: " + password);
    }
}
```

### 3. Static content in Spring Boot Application

By default, Spring Boot will load static resources from `../static` directory folder in the proejct src.

In this folder, some of example of static resources like HTML files, CSS, Javascript files and images etc...

**Notes:** Do not use the `src/main/webapp` directory if your application is packaged as a JAR. Although this is a standard Maven directory, it works only with WAR packaging. It silently ignored by most build tools if you generate a JAR.

### 4. Template in Spring Project

Spring Boot includes auto configuration for following template engines

Some of template engines we use is
- FreeMarker
- Thymeleaf
- Mustache

And by the defaults, Spring Boot will load templates from `../templates` directory. And Thymeleaf is one of the most popular template engine, we will use in this course.

### 5. Unit test in Spring Project

Spring Boot unit test class will automatically create by `Spring Initializr` when you create the first project in this websites.

You can add the unit test in the file that auto generate.