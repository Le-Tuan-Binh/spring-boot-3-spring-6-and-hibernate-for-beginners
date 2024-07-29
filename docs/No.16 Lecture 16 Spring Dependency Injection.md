## Dependency Injection

The dependency injection inversion principle, the client delegates to another project the responsibility of providing its dependencies.

### 1. Injection Type

There are multiple types of injection with Spring. We will cover two recommended types of injections
- Constructior Injections 
- Setter Injections

And the problems is which `injection type` we need to use?

**Constructor Injection**

- Use this when you have required dependencies.

- This is also generally recommended by the spring.io development team as the first choice.

**Setter Injection**

- Use this when you have optional dependencies.

- If dependency is not provided, your app can provide reasonable default logic 

### 2. Spring AutoWiring 

For dependency injection, Spring can use autowiring. Spring will look for a class that matches, for example, matches by types: class or interface. 

Spring will inject it automatically, ... hence it is autowired.

For example, when we inject a `A` implementation, Spring will scan for `@Components` hey any one implements the `A` interface. If so, let's inject them. For example we can inject to `A1`. 

### 3. `@Component` Annotation

`@Component` marks the class as a `Spring Beans`. A Spring Beens is just a regular Java class that is managed by Spring.
 
`@Component` also makes the bean available for dependency injection.

### 4. Development Process - Constructor Injecttion

1. Define the dependency interface and class.
2. Create a REST Controller.
3. Create a constructor in your class for injection.
4. Add `@GetMapping` for `/...`

#### 4.1 Define the dependency interface and class

First create the file `Coach.java` and `CricketCoach.java` implement from the `Coach.java`.

And in the class `CricketCoach.java` need to have `@Components` annotation marks the class as a Spring Bean and make it into a cadidate for the dependency injection.

**CricketCoach.java**

```java
import org.springframework.stereotype.Component;

@Component
public class CricketCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15 minutes";
    }
}
```

**Coach.java**

```java
public interface Coach {
    String getDailyWorkout();
}
```

#### 4.2 Create a CoachController REST Controller

**CoachController.java**

```java
import org.springframework.web.bind.annotation.RestController;

@RestController
public class CoachController {

}
```

#### 4.3 Create a Constructor in your class for injection

```java
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public CoachController(Coach coach) {
        this.coach = coach;
    }
}
```

The `@Autowired` annotations tells Spring to inject a dependency, If you have one constructor then `@Autowired` on constructor is optional. At the moment we only have one Coach implementation CricketCoach so Spring can figure this out. In later we will cover the case of multiple Coach implementations.

#### 4.4 Add `@GetMapping` for `/...`

```java
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public CoachController(Coach coach) {
        this.coach = coach;
    }
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```