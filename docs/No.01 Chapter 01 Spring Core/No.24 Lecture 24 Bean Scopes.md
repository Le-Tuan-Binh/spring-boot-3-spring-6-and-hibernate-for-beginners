## Bean Scopes in Spring Boot Application

Scopes refers to the lifecycle of the Beans. How long does the Bean live? and How many instances are created? and How is the bean shared.

### 1. Default Scope

The default scope of Bean in Spring is `Singleton`. So what is the `Singleton`

- Spring container creates only one instances of the bean, by the default it cached in memory and all dependency injection for the beans will reference the **SAME** beans.

So to illustrate for it, we will modify the controller to see the theory in here.

```java
@RestController
public class CoachController {
    private Coach coach;
    private Coach anotherCoach;
    @Autowired
    public CoachController(@Qualifier("cricketCoach") Coach coach,
                           @Qualifier("cricketCoach") Coach anotherCoach) {
        this.coach = coach;
        this.anotherCoach = anotherCoach;
    }
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```

In this case, both the `anotherCoach` and `coach` point to the same instance.

### 2. Explicitly Specify Bean Scope

We can also define the scope of the Bean in this class like the code below, we determine the Scope of the class in the definition of the class.

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
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

### 3. Additional Spring Bean Scopes

Here are more Spring Bean Scopes you can see more in the Springs documents. Here is a summary in the table for you can see more quickly.

![alt text](/images/image-06.png)

### 4. Prototype Scope Example

**Prototype Scope:** new object instances for each injection in the Spring Applications.

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
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

To see the result to ensure that we have the another instances for each injection we need to add the code below into the controller.

```java
@GetMapping("/check")
public String checkCoach() {
	return "Comparing beans: coach === anotherCoach, " + (coach == anotherCoach);
}
```

Now when we access to the endpoint `/check` we can see the text display in the screen

```bash
Comparing beans: coach === anotherCoach, false
```

**Singleton Scope:** only one object instances create for all injection in the Spring Applications.

So if we set the scope is `SCOPE_SINGLETON`, we can see the code below

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
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

Go to the endpoint again, we can see the text display in the screen is

```bash
Comparing beans: coach === anotherCoach, true
```

