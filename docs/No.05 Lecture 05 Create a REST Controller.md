## Spring Boot - Create a REST Controller

### 1. Create a REST Controller

Create a new Java class in your project. For instance, let's name it `SpringRestController.java`.

This class will handle HTTP GET requests to the root URL `("/")` and return a simple `"Hello World!"` message.

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class SpringRestController {
    @GetMapping("/")
    public String sayHello() {
        return "Hello World!";
    }
}
```

In this setup, we use the `@RestController` and `@GetMapping` `annotations`. These `annotations` play `crucial roles` in defining the behavior of the REST controller.

> **`@RestController` Annotation**

**Definition:** The `@RestController annotation` is a specialized version of the @Controller annotation. It is a convenience annotation that **combines** `@Controller and @ResponseBody`, eliminating the need to annotate every request handling method with `@ResponseBody`.
**Purpose:** It indicates that the class is a REST controller where each method returns a domain object instead of a view. The response is automatically serialized into JSON or XML and sent back to the client.

> **`@GetMapping` Annotation**

**Definition:** The `@GetMapping annotation` is a composed annotation that acts as a shortcut for `@RequestMapping(method = RequestMethod.GET)`.
**Purpose:** It is used to map HTTP GET requests to specific handler methods. In this example, it maps GET requests to the root URL **("/")** to the `sayHello` method.

### 2. Spring Boot Project Structure

Spring Boot project use the Maven Standard Project Structure so it will divided into some basic folder below

- src/main/java: This is an folder to store your Java code for your project.
- src/main/resources: Properties, Config files used by your apps.
- src/main/webapp: JSP Files and web config files other web assets (image, css, js, etc...)
- src/test: Unit testing code and properties.
- target: Destination directory for compiled code, automatically created by Maven.