## Scanning For Component Classes

Spring will scan your Java classes for special annotations. For example `@Component`, etc... It automatically register the beans in the Spring Container.

In the main file of application running `Main.java`

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
public class Main {
	public static void main(String[] args) {
		SpringApplication.run(Main.class, args);
	}
}
```

The Annotation `@SpringBootApplication` is enables to auto configurations `Component Scanning`. It is Additional Configuration.

And in behind the scenes, this annotation is composed of following annotations: `@EnableAutoConfiguration`, `ComponentScan`, `Configuration`.

### 1. `@SpringBootApplication` Annotation

| Annotation               | Description                                                                           |
|--------------------------|---------------------------------------------------------------------------------------|
| @EnableAutoConfiguration | Enable Spring Boot's auto-configuration support                                       |
| @ComponentScan           | Enables component scanning of current package. It also recursively scans sub-packages |
| @Configuration           | Able to register extra beans with @Bean or import other configuration classes         |

### 2. SpringApplication.run

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
public class Main {
	public static void main(String[] args) {
		SpringApplication.run(Main.class, args);
	}
}
```

This allow the application to bootstrap your Spring application, and then we give a reference here to the actual name of our class. In this case is `SpringApplication`.

Behind the scenes, it creates application context and registers all beans. Starts the embedded server like TomCat, etc...

### 3. More on Component Scanning

By default, Spring Boots Starts components scanning from same packages as your main Spring Boot Application, and also scans sub-packages recursively.

This implicity defines a base search packages

- Allow you to leverage default component scanning.
- No need to explicitly reference the base package name.

### 4. Common Pitfall, Different Location

By default, Spring Boot will not component scan these packages. Only the package of `main` Spring Boot applications class and sub-packages.

The default scanning is fine if everything is under the package of the main, but how if the project have many other packages like `utils`, `org.personal.tbin`, or `edu.vn.hcmus`. How will this kind of work out and how we can configure this accordingly.

So in here you can in your Spring Boot application Annotation, you can choose the `scanBasePackages` of your Spring project. It will choose the explicity list the base packages we need to scanning in this project like the code below.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication(
	scanBasePackages ={
		"com.example.utils;",
		"org.personal.tbin",
		"edu.vn.hcmus"
	}
)
public class SpringBootV1Application {
	public static void main(String[] args) {
		SpringApplication.run(SpringBootV1Application.class, args);
	}
}
```

