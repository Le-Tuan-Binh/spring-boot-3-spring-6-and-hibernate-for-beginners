## Setter Injection in Spring Project

There are two `Spring Injection Type` is `Constructor Injection` and `Setter Injection`.

### 1. Setter Injection:

It is a method ineject dependencies by calling setter method(s) on your class.

Now let take a look into the example belows about the `Autowiring`. Injecting a `Coach` implementation, Spring will scan for `@Components`, It will find any one implements the `Coach` interface. So Let's inject them. For example: `CricketCoach`

### 2. Development Process

- First you need to create setter methods in your class for injections.

- Then we need configure the dependency injection with `@Autowired` Annotation.

#### 2.1 Create setter methods in your class for injections

```java
import com.example.spring_boot_v1.model.Coach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CoachController {
    private Coach coach;
    public void setCoach(Coach coach) {
        this.coach = coach;
    }
}
```

#### 2.2 Configure the dependency injection with Autowired Annotation

```java
import com.example.spring_boot_v1.model.Coach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public void setCoach(Coach coach) {
        this.coach = coach;
    }
}
```

In behind the scences, Spring will create the code below

```java
Coach coach = new CricketCoach();
CoachController controller = new CoachController();
controller.setCoach(coach);
```

Now we can also inject the dependencies by calling `ANY` method on your class, just simply give `@Autowired`

```java
 @Autowired
    public void setCoach(Coach coach) {
        this.coach = coach;
    }

    @Autowired
    public void doSomeStuff(Coach coach) {
        this.coach = coach;
    }
```

### 3. Injection Types, which one to use ?

**Constructor Injection**

- Use this when you have required dependencies

- Generally recommended by the `spring.io` development team as first choice.

**Setter Injection**

- Use this when you have optional dependencies

- If dependency is not provided, your app can provide reasonable default logic 