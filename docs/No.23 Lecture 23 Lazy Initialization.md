## Lazy Initialization

By the default, when your application starts, all beans are initialized like `@Component`, etc...

Spring will create an instance of each and make them available.

You can test by give the code below in each class

**TrackCoach.java**
```java
import org.springframework.context.annotation.Lazy;
import org.springframework.stereotype.Component;
@Component
@Lazy
public class TrackCoach implements Coach {
    public TrackCoach() {
        System.out.println("In constructor: " + getClass().getSimpleName());
    }
    @Override
    public String getDailyWorkout() {
        return "Run a hard 5km !!!";
    }
}
```

**TennisCoach.java**
```java
@Component
public class TennisCoach implements Coach {
    public TennisCoach() {
        System.out.println("In constructor: " + getClass().getSimpleName());
    }
    @Override
    public String getDailyWorkout() {
        return "Practice your backhand volley !!!";
    }
}
```

**CricketCoach.java**
```java
import org.springframework.stereotype.Component;
@Component
public class CricketCoach implements Coach {
    public CricketCoach() {
        System.out.println("In constructor: " + getClass().getSimpleName());
    }
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
    public BaseballCoach() {
        System.out.println("In constructor: " + getClass().getSimpleName());
    }
    @Override
    public String getDailyWorkout() {
        return "Speed 30 minutes in batting practices !!!";
    }
}
```

Now when you run the program you will see the display in the run console like below

```bash
In constructor: BaseballCoach
In constructor: CricketCoach
In constructor: TennisCoach
In constructor: TrackCoach
```

Instead of creating all beans up font, we can specify lazy initialization. A bean will only be initialized in the following cases:

- It is needed for dependency injection
- Or it is explicitly requested

Add the `@Lazy` annotation to a given class.

So here is the example for this `@Lazy` Initialization by the code below, just look for

```java
import org.springframework.context.annotation.Lazy;
import org.springframework.stereotype.Component;
@Component
@Lazy
public class TrackCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Run a hard 5km !!!";
    }
}
```

When this, the Bean only initialized if needed for dependency injection. If not needed it will not created.

So now when we run the program the only we see in the run console is

```bash
In constructor: CricketCoach
In constructor: BaseballCoach
In constructor: TennisCoach
```

So to configure other beans for lazy initialization, we would need to add `@Lazy` to each class.

But turn into tedious work for a large number of classes, i wish we could set a global configuration property.

### 1. Lazy Initialization in Global Configuration

Go to the `application.properties` and add the code below

```java
# Config the lazy-initialization
#
spring.main.lazy-initialization=true
```

So all beans are lazy, no beans are created until needed. Once we acess REST endpoint, Spring will determine dependencies for controller.

For dependency resolution, Spring create `instance of the beans` in the controller need first then create instances of `controller` and inject the beans into the controller.

Now you can add a new line to see the working of the Spring Application in the controller like below.

```java
@RestController
public class CoachController {

    private Coach coach;

    @Autowired
    public CoachController(@Qualifier("cricketCoach") Coach coach) {
        System.out.println("In constructor: " + getClass().getSimpleName());
        this.coach = coach;
    }

    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```

And when you access to the endpoint, you can see in the run console of the Spring project like below

```bash
In constructor: CricketCoach
In constructor: CoachController
```

### 2. Lazy Initialization 

**Advantages**

- Only create objects as needed

- May help with faster startup time if you have large number of components

**Disadvantages**

- If you have web related components like `@RestController`, not created until requested.

- May not discover configuration issues until too late

- Need to make sure you have enough memory for all beans once created.

In the default, Lazy Initialization feature is disabled by default. You should profile your application befor configuring lazy initialization. Avoid the common pitfall of premature optimization.
