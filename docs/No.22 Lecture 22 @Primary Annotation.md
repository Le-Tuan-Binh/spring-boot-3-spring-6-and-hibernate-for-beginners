## `@Primary` Annotation in Spring Boot

In the case of multiple Coach implementations

[alt.img](/images/image-05.png)

We can resolved it using `@Qualifier` Annotation by specified a coach by name.

Instead of specifying a coach by name using `@Qualifier`, i simply need a coach but i don't care which coach if there are multiple coaches, then you coaches figure it out and tell me who's the **primary** coach.

So now you need to add the `@Primary` Annotation into the class implentation from Coach which you want to default. For example the code below, i will add into the `TrackCoach.java`

```java
import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;
@Component
@Primary
public class TrackCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Run a hard 5km !!!";
    }
}
```

After then, your controller only need to be like the code below, and it will running without any warning or error.

```java
import com.example.spring_boot_v1.model.Coach;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
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

When using `@Primary` can have **only one** for multiple implementations.

If you mark multiple classes with `@Primary`, we have the problems below

```bash
Unsatisfied dependency expressed through constructor parameter 0: No qualifying bean of type 'com.example.spring_boot_v1.model.Coach' available: more than one 'primary' bean found among candidates:[baseballCoach, cricketCoach, tennisCoach, trackCoach]
```

### 1. Mixing the `@Primary` and `@Qualifier`

If  you mix `@Primary` and `@Qualifier` you need to noice that

- `@Qualifier` has the higher priority 

So if you have a `@Primary` in another class, but you have the `@Qualifier` it will choose the class that the `@Qualifier` because it have the higher priority.

So we will consider that **Which one: @Primary or @Qualifier**

- `@Primary` leaves it up to the implementation classes and it could have the issue of multiple `@Primary` classes leading to an error.

- `@Qualifier` allows to you be very specific on which bean you want.

So in general, i recommend using `@Qualifier`, because it will more specific and higher priority.