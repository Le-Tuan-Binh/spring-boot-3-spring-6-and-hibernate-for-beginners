## Spring Boot Starters

This is a curated list of Maven dependencies to develope a new Spring Boot Project with Maven more easily.

This is a collection of dependencies grouped together, by tested and verified by the Spring Development team. 

Make it much easier for the developer to get started with Spring, it reduces the amount of Maven configuration.

### 1. What is in the Starter?

For the Intellij Users, Select View -> Tool Windows -> Maven Projects > Dependencies

### 2. Spring Boot Starter Parent

Spring Boot provides a `Starter Parent`, this is a special starter that proivides Maven defaults.

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>3.3.1</version>
  <relativePath/>
</parent>
```

Maven defaults defined in the Starter Parent

- Default compiler level
- UTF8 Source Encoding
- and the Other...

To override a default, set as a property

```xml
<properties>
  <java.version>22</java.version>
</properties>
```

For the `spring-boot-starter-*` dependencies, we will no need to list version, it will inheritance from the parent which is Starter Parents. So you no need to list individual versions. It is a good way to maintenance!

Default the configuration of Spring Boot Plugin is 

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```

Now open your terminal, run the command line bellow

```bash
mvn spring-boot:run
```

**So the benefit of the Spring Boot Starter Parent**

- Default Maven configuration: Java Version, UTF-encoding etc
- Dependency management
  - Use version on parent only.
  - `spring-boot-starter-*` dependencies inherit version from parent.
- Default configuration of Spring Boot plugin.