## Getting Started

This course covers the LATEST VERSIONS of Spring Boot 3, Spring 6 and Hibernate 6!

You will learn about: Spring Boot Core, Spring Boot MVC, Spring Boot Security, Spring Boot REST API, Spring Data JPA, Spring Data REST, Thymeleaf, AOP and Hibernate/JPA ... all connected to a MySQL database

By the end of this course, you will create all of the source code for a complete Spring Boot REST APIs for a full CRUD REST API real-time project.

About this course please see in [Spring Boot 3, Spring 6 & Hibernate for Beginners](https://github.com/darbyluv2code/spring-boot-3-spring-6-hibernate-for-beginners). This is a repository of this course, any thing please contact to me.

## Getting Involved

### 1. Spring Boot 3, Spring 6 & Hibernate for Beginners

#### 1.1. Spring Boot and Spring

**Spring** is a comprehensive framework for building Java applications, offering features like dependency injection, aspect-oriented programming, and robust support for enterprise technologies such as JDBC, JPA, and more.

It provides a modular approach to building applications, encouraging best practices and design patterns that promote maintainability and scalability.

**Spring Boot**, on the other hand, is built on top of Spring and aims to simplify the development process by providing a set of conventions and pre-configurations.

It eliminates much of the boilerplate configuration that developers would typically need to set up a Spring application, such as configuring dependencies, setting up servers, and defining application contexts.

Spring Boot use Spring behind the secenes, Spring Boot simply make it easier to use Spring:

- Make it easier to get started with Spring development

- Minimize the amount of manual configuration

- Perform auto-configuration based on props files and JAR classpath

- Help to resolve dependency conflicts (Maven or Gradle)

- Provide an embedded HTTP server so you can get started quickly like TomCat, Jelly, Undertow...

#### 1.2. Spring Initializr

First go to the website [Spring Initializr](https://start.spring.io/), this website will help you to create a starter Spring Boot Project more quickly. Reduces the time and effort required to set up a new Spring Boot project by providing a user-friendly interface to customize project details and dependencies.

1. Select your dependencies.

2. Creates a Maven/Gradle Project.

3. Import the project into your IDE (Eclipse, Intellij, NetBBeans..etc..)

#### 1.3. Running the Spring Boot Apps

Spring Boot Apps can be run standalone (It includes embedded server in their selfs).

**Run the Spring Boot app from the IDE or Command Line.**

```bash
java -jar <jar_name>.jar
```

Spring Boot's ability to run standalone applications with embedded servers and its ease of deployment from both IDEs and command line interfaces make it a powerful choice for developing modern Java applications. Whether you're building microservices, web applications, or RESTful APIs, Spring Boot provides the tools and capabilities to streamline your development and deployment workflows effectively.

#### 1.4. Deploying Spring Boot Apps

Spring Boot applications can be packaged as WAR files for deployment to external servlet containers like Tomcat, JBoss, WebSphere, and others. This approach allows you to leverage existing infrastructure and server configurations while still benefiting from Spring Boot's productivity features.

Deploy **WAR File (Web Application Archive)** to an **External Server**: TomCat, JBoss, WebSphere etc...

#### 1.5. Maven Project in Java

When building your Java Project, you may need additional JAR Files, For example: Spring, Hibernate, Commons Logging, JSON etc...

One approach is to download the JAR files from each project website. Or manually add the JAR files to your build path / classpath.

So we will use **Maven Solution**

- Tell the Maven the projects you are working with dependencies: Spring, Hibernate etc...
- After that Maven will go out and download the JAR files for those projects for you, and Maven will make those JAR files available during compile and run.

#### 1.6. Development Process

Just working step by step, you will create the first Spring Boot project

1. Configure our project at [Spring Initializr](https://start.spring.io/)

- Project: In this, you can choose depend on your demand, in this course we will use **Maven Project**.

- Language: In this course, the main languages we use is **Java**.

- Spring Boot: This is one of the most important things we need to considered. In this option, you need choose the latest released version of Spring Boot. But please avoid the **Snapshot** versions since it is the alpha and beta version of this Spring Boot.

- Project Metadata: In this, you will setting the name of your project and some of basic and important information for your source and project.

  - Group: This typically represents the base package name for your project. It often follows the reverse domain name convention (e.g., com.example).
  - Artifact: The artifact ID is the name of the project or module within the group. It uniquely identifies your project within the repository. (e.g., my-spring-app)
  - Name: The display name of your project. This is a human-readable name that identifies your project.
  - Description: A brief summary or description of your project's purpose and functionality.
  - Package name: The base package namespace for your Java classes. It is recommended to use a meaningful and descriptive package structure.
  - Packaging: Specifies whether the project should be packaged as a **JAR** (Java ARchive) or a **WAR** (Web Application ARchive) file.
  - Java: Specifies the Java version compatibility for your project. Spring Boot supports various Java versions depending on the Spring Boot version used.

- Add Dependencies: In this, click into and search the key word `Spring web` and choose the `Spring Web` to development the Spring Boot apps with **TomCat** and **Spring MVC**.

2. Download the zip file: Just click into the button **Generate** to create the zip file of sources code from the website.

3. Unzip the file

4. Import the project into our IDE.

#### Frequently Asked Questions

```bash
1. Does Spring Boot replace Spring MVC, Spring Rest etc... ?
```

No. Instead, Spring Boot actually uses those technologies.

```bash
2. Does Spring Boot run code faster than regular Spring Code?
```

No, Behind the scenes, Spring Boot uses same code of Spring Framework.

So remember, spring boot is about making it easier to get started like minimizing configuration etc...
