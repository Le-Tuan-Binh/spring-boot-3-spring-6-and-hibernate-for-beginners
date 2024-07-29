## Inversion of Control (IoC)

Inversion of Control is the approach of outsourcing the construction and management of objects.

### 1. Coding Scenario

The application should be configurable, and easily to change.

So we can go to the **ideal solution** for this problems. First your application send an request to the `Object Factory` that give an **A Object**, In the factory will configurable and determine which object will be create and send return to the application.

In this case, `Spring` like an `Object Factory`. We can know that is `Spring Container`.

![alt text](/images/image-04.png)

Spring Container have two primary function

- Create and manage objects (Inversion of Control)
- Inject Object dependencies (Dependency Injection)

## 2. Configuring Spring Container

This is have many way to configuring the Spring Container like an **XML configuration file (legacy)**, **Java Annotations (modern)** or by **Java Source Code (modern)**.

In the real world, we are use mostly two way modern by Java Annotation and Java Source Code, the XML configuration file is not use exits more.

