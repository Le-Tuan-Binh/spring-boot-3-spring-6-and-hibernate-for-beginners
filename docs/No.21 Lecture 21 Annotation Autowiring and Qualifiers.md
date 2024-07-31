## Annotation Autowiring and Qualifiers

When we injecting a `Coach` implementation, Spring will scan `@Components`, and if anyone have implements the `Coach` interface, it will auto inject them. But the question is if we have many class implement the `Coach` interface which one the Spring is choose.

![alt text](/images/image-05.png)

We can implement the code below

**CricketCoach.java**
```java
import org.springframework.stereotype.Component;
@Component
public class CricketCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15 minutes !!!";
    }
}
```

**BaseballCoach.java**
```java
import org.springframework.stereotype.Component;
@Component
public class BaseballCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Speed 30 minutes in batting practices";
    }
}
```

**TrackCoach.java**
```java
import org.springframework.stereotype.Component;
@Component
public class TrackCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Run a hard 5km !!!";
    }
}
```

**TennisCoach.java**
```java
import org.springframework.stereotype.Component;
@Component
public class TennisCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice your backhand volley !!!";
    }
}
```

Now we have a little problems, the parameter 0 of constructor in `com.example.controller.CoachController` require a single Bean, but 4 we found: baseballCoach, cricketCoach, tennisCoach, trackCoach.

So the solution is `Be specific` using the `@Qualifier` Annotation.

## 1. @Qualifier Annotation with Constructor Injection

We need to use the `@Qualifier` Annotation to specify the bean id like the code below, **The Bean ID is same name of class, first character lower-case**

```java
import com.example.spring_boot_v1.model.Coach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public CoachController(@Qualifier("cricketCoach") Coach coach) {
        this.coach = coach;
    }
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```

So the other Beans ID we can use in this case is: baseballCoach, trackCoach, tennisCoach.

## 2. @Qualifier Annotation with Setter Injection

If you are using `Setter Injection`, can also apply `@Qualifier` annotation. Just look into the code below like an example.

```java
import com.example.spring_boot_v1.model.Coach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public void setCoach(@Qualifier("cricketCoach") Coach coach) {
        this.coach = coach;
    }
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```
