## Field Injection with Annotations and Autowiring

### 1. Spring Injection Types

It is recommended by the `spring.io` development team.

- Constructor Injection: It required dependencies

- Setter Injection: Optional dependencies

Now the Spring Injections Types is not recommended by the `spring.io` development team it is `Field Injection`

### 2. Field Injection

In the early days, field injections was popular on Spring project. But in the recent years, it has fallen out of favor.

In general, it makes the code harder to unit test. As a result, the spring.io team does not recommended field injection. However, you will still see it being used on legacy projects.

Inject dependencies by setting field values on your class directly, even private field. But it is `Accomplished by using Java Reflection`

**So in step 1: Configure the dependency injection with Autowired Annotation**

This is the code below is an example

```java
@RestController
public class CoachController {
	@Autowired
    private Coach coach;
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```

In this example, we don't need the constructor or setter, we will add the `@Autowired` annotation into the private field. So it call the `field injection`.






