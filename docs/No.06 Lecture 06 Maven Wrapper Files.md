## Maven Wrapper Files

The `Maven Wrapper Files` is files you can see in your source project which is name that `mvnw` and `mvnw.cmd`. This file allows you to run a Maven project. That mean no need to have Maven installed or present on your path.

If correct version of Maven is NOT found on your computer, it automatically downloads correct version and runs Maven from the internet. Two file are provided for you

- mvnw.cmd for Microsoft Windows. You can use the command line below

```bash
mvnw clean compile test
```

- mvnw.sh for Linux or Mac OS

```bash
$ ./mvnw clean compile test
```

In terms of basic idea, it is a program that wraps the maven download process for your computer if your computer does not have maven available or downloads the appropriate Maven version for you.

If your computer have exits the Maven you can delete it from your source code of project. To check your computer have Maven or not please open the cmd and type `mvn --version`, if you can see it like below, it mean you already have Maven in your environment.

```bash
C:\Users\User> mvn --version
Apache Maven 3.9.8 (36645f6c9b5079805ea5009217e36f2cffd34256)
Maven home: D:\Applications\apache-maven-3.9.8-bin\apache-maven-3.9.8
Java version: 22.0.1, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jdk-22
Default locale: en_US, platform encoding: UTF-8
OS name: "windows 11", version: "10.0", arch: "amd64", family: "windows"
```

Then you can remove the `mvnw` and `mvnw.cmd` in your project source, use some command line to test the mvn with your project

```bash
mvn clean compile test
```