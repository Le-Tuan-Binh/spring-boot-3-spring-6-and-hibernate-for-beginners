## Application Properties in Spring Boot Project

The problems is you need for your app to be configurable... no hard-coding of value, and you need to read app configuration from a properties file.

The solution for this is use the `application.properties` file. By default, Spring Boot reads information from a standard properties file. Located at `/src/main/resources/application.properties`.

You can defined any custom properties in this file and the Spring Boot app can access properties using `@Value` annotation.

### 1. Development Process

- Define custom properties in `application.properties` 

- Inject properties into Spring Boot Application using `@Value`

### 2. Define custom application properties

Now you will go the direction `/src/main/resources/application.properties` and add the custom properties for your Spring Boot Project like the code below

```xml
# Configure Your Own Props
#
user.name=Le Tuan Binh
user.password=ltbinh
```

It no has limit for you to define the application properties. Now we will go to the next step that is Inject properties into Spring Boot Application.

### 3. Inject properties into Spring Boot Application

```java
@RestController
public class SpringRestController {

    @Value("${user.name}")
    private String username;

    @Value("${user.password}")
    private String password;
	
    @GetMapping("/")
    public void printAccount() {
        System.out.println("Username: " + username);
        System.out.println("Password: " + password);
    }
}
```

You use the `@Value` annotation to use the value in the `application.properties` withou any more code needed.

