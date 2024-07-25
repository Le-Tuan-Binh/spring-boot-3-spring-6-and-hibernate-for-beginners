## Spring Boot with Maven Project

### 1. What is Maven ?

Maven is a Project Management tool, most of popular use of Maven is for build management and dependencies.

When building an Java project, you may need many additional JAR files, for example: Spring, Hibernate, Commons Logging and JSON etc...

One of the traditional approach is to download the JAR file from each project website and then manual add the JAR files to your build path / classpath.

So just thinking if you are developer, you need go to each website of each JAR file to download and manual add each into your project. It very match many problems when the version is change or something. So **Maven Project** can help you manage it easily.

The Maven tell the project which dependencies the project are working with like Spring, Hibernate etc... Maven will go out and download the JAR files automatically for those project for you. It also make the JAR files is available during compile and run.

Just look at the image below, you can have the good look how maven work with your apps when compile and run.

![How it work Maven ?](/images/image-01.png)

When it retrieves a project dependency, it will also download supporting dependencies, for example: Spring depends on the common-logging... So when you give Maven to use Spring, it will be automagically download the common-logging for your project.

### 2. Standard Directory Structure

Normally, when you join to a new project, each development team dreams up their own directory structure, so it very not ideal for new commer and not standardized. So Maven give the standard directory structure.

```bash
└───maven-project
  ├───pom.xml
  └───src
      ├───main
      │   ├───java
      │   ├───resources
      │   ├───filters
      │   └───webapp
      ├───test
      │   ├───java
      │   ├───resources
      │   └───filters
```


So we will need to know which directory is doing for what, by the description below we can have the overview of each folder in project.

- src/main/java: This is an folder to store your Java code for your project.
- src/main/resources: Properties, Config files used by your apps.
- src/main/webapp: JSP Files and web config files other web assets (image, css, js, etc...)
- src/test: Unit testing code and properties.
- target: Destination directory for compiled code, automatically created by Maven.

If you are working with the web apps project, you will put your asset in the `src/main/webapp`. In this you will place the `JSP` files, or any `configuration` files, `CSS` files and images and so on.

```bash
maven-project/
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── maven-project/
│   │   │               ├── maven-project.java
│   │   │               └── ...
│   │   ├── resources/
│   │   │   └── application.properties
│   │   ├── webapp/
│   │       ├── WEB-INF/
│   │       │   ├── web.xml
│   │       │   └── ...
│   │       ├── META-INF/
│   │       │   └── context.xml
│   │       └── static/
│   │           ├── css/
│   │           │   └── style.css
│   │           ├── js/
│   │           │   └── script.js
│   │           └── index.html
│   └── test/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── maven-project/
│       │               ├── maven-project.java
│       │               └── ...
│       └── resources/
├── target/
└── ...
```

The benefit of this structure folder is: It is easy for new developer joinning a projedts. They can easily find code, properties file, unit test, web file etc...

### 3. Maven Key Concepts

**POM (Project Object Model)**: Configuration file for your project, and always located in the root of your Maven project.

**POM File Structure**: POM file structure include three important information in the `pom.xml`, now we will see detail each information.

- `project meta data`: It include the Project name, Version and Output File Type: JAR, WAR, etc...

- `dependencies`: This is list of projects we depend on like Spring, Hibernate, etc...

- `plug-ins`: Additional custom tasks to run like generate JUnit test report, etc...

Some of the basic simple `pom.xml` file you can see below

**Project coordinates:** The project coordinates uniquely identify the project and are used to manage dependencies. The **group ID**, **artifact ID**, and **version** number must be specified.

| Name        | Description                                                                                                   |
|-------------|---------------------------------------------------------------------------------------------------------------|
| Group ID    | Name of company, group or organization. Convention is use to reverse domain name **com.example**              |
| Artifact Id | Name for this project                                                                                         |
| Version     | A specific release version like: **1.0, 2.0**... If project is under active development then **1.0-SNAPSHOT** |

```xml
<groupId>com.example</groupId>
<artifactId>my-project</artifactId>
<version>1.0.0</version>
```

**Dependencies**: This section lists all the dependencies required by the project. Maven automatically downloads and includes these dependencies in the project.

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
  </dependency>
</dependencies>
```

**Build configuration**: This section specifies how the project should be built and includes information such as the project’s source code directory, output directory, and any plugins required for the build.

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

**Plugins**: Maven plugins are used to extend the build process. This section lists all the plugins required by the project.

```xml
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
</plugin
```

**GAV(GroupID - ArtifactId - Version)**: You can see some of this referred in some books or document to make it more easily to read and not too long to remember.

You can find the dependencies coordinates you want with 2 option. The first option is go to the website of each dependencies and get each them or you can find all thing in [Maven Central Repository](https://central.sonatype.com/) it will be easily to find and download then the option 1.