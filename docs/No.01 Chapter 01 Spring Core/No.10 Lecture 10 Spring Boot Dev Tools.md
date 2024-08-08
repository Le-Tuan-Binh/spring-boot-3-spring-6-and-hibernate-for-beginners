## Spring Boot Dev Tools

The main problems is when running Spring Boot Applications, if you make changes to your source code, then you have need to manually restart your application. It is not good for developer to change something.

Here is one of the solution: `Spring Boot Dev Tool`, we can use it to rescue this problems. It automatically restarts your application when code is updated.

To use it, you only need to add the dependency to your POM Files, no need to write additional code. For the Intellij, need to set additional configurations.

**In the Intellij, add the dependency to your POM files**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

But the problems is in the Intellij Community Edition does not support the DevTools by default, so we need to make some configurations in the Intellij.

**Select: Preferences > Build, Excution, Deployment > Compiler**, check the box **Build project automatically**

Not only that, we need to do some additional setting here:

**Select: Preferences > Advanced Settings**, check into the box **Allow auto-make to...**

**Development Process of Project have SpringBoot Dev Tools**

- Apply Intellij configurations

- Edit `pom.xml` and add `spring-boot-devtools`

- Add new REST endpoint to our app

- Verify the app is automatically reloaded