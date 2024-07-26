## Run the Spring Boot project from Command Line

During development, we spend most time in the IDE, however we may want to run the Spring Boot project outside of the IDE. So one of the method is run from the Command Line.

### 1. Running from the Command Line

When running from the command line, we no need to open the IDE. Since we use a Spring Boot, the server is embedded in JAR file. So we no have to separate server installed/running because the spring boot app are self-contained. 

In the jar file, it include your application code and include the server, it is self-contained unit so we not need to install anythings.

You will have two-option to run the project from command line

- Option 1: Use `java -jar`

- Option 2: Use the Spring Boot Maven Plugin `mvnw spring-boot:run`

### 2. Run use the `java -jar` in command line

The syntax is 

```bash
java -jar <name-of-your-project>.jar
```

It will auto start the application and start the embedded server (Tomcat), it self-contained nothing else to install.

### 3. Run use the Spring Boot Maven Plugin

`mvnw` allows you to run a Maven Project, it no need to have Maven installed or present on your path. If correct version of Maven is not found, it will **Automatically download** correct versions and run the Mavens. Two file a provided is
- mvnw.cmd: Maven for window.
- mvnw.sh : Maven for Linux/Mac.

Now you will go to the command line and use the syntax below

```bash
mvnw clean compile test
```

If you already have Maven installed previously, then you can delete the file `mvnw` and just use the Maven as you normally would 

```bash
mvn clean compile test
```

When you first create the Spring Boot Project, it will automatically add the plugin into your build like code below.

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

It use to package excutable `jar` or `war` archive, so it can easily run the application.

You can run the Spring project with the syntax below

```bash
mvwn package
mvwn spring-boot:run
```

or if you already have Maven

```bash
mvn package
mvn spring-boot:run
```





