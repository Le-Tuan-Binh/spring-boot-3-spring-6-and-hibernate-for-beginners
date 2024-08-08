## Spring MVC Application

For example, when building a Spring MVC app, you mormally need many dependencies but the solution is not add all the dependencies, we only need `spring-boot-starter-web`, it provide many things include the all thing need to working with Spring MVC

```java
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

The `Spring Boot Starter` not only include the Spring MVC, it is a collections of Maven dependencies like `spring-web`, `srping-webmvc`, `hibernate-validator`, `json`, `tomcat`...

It save the time for developer from having to list all of the individual dependencies. Also, makes sure you have compatible versions.

**More complex Spring Application**

If  we are building a Spring app that needs: Web, Security..., Simply select the dependencies in the `Spring Initializr`, it will add the appropriate `Spring Boot starters` to your pom.xml.

![alt text](/images/image-02.png)

Some of famous Spring Boot Starters from the Spring Development Team is

| Dependencies                 | Description                                                                           |
|------------------------------|---------------------------------------------------------------------------------------|
| spring-boot-starter-web      | Building web apps, includes validation, REST, Uses Tomcat as default embedded server. |
| spring-boot-starter-security | Adding Spring Security support                                                        |
| spring-boot-starter-data-jpa | Spring database support with JPA and Hibernate                                        |