## Constructor Injection Behind the Scenes

### 1. How Spring Processes your application

The spring framework will perform operations behind the scenes for you. Behind the scenes, Spring will create a new instance of your `Coach` and `CricketCoach`. It also perform constructor injection with your `CoachController`.

In the Spring Framework
```java
Coach coach = new CricketCoach();
CoachController controller = new CoachController(coach);
```

### 2. The `new` keyword ... is that it ?

You may wonder that, is it just the `new` keyword, and you don't need Spring do it for this.

But it not is only the new keyword. Spring is more than just `Inversion of Control and Dependency Injection`. For small basic apps, it may be hard to see the benefits of Spring.

### 3. Spring for Enterprise applications

Spring is targeted for enterprise, real time and real world applications. Spring provides features as 

- Database access and Transactions
- REST APIs and Web MVC Structure
- Security
- etc...



