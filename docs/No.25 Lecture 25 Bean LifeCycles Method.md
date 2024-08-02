## Beans LifeCycles Method Annotation

Here is the high level view of the bean lifecycle when the Spring Container Started. Beans are instantiated, dependencies are injected, internal Spring Processing and Bean is ready for use in the stage Your Custom Init Method.

And when the container of application is shutdown or stop, your custom destroy method will be called.

![alt text](/images/image-07.png)

## 1. Bean LifeCycle Methods or Hooks

You can add custom code during `bean initialization`

- Calling custom bussiness logic methods.
- Setting up handles to resources (database, socket, file etc...)

You can add custom code during `bean destructor`

- Calling custom bussiness logic method
- Clean up handles to resources (database, socket, file etc...)

### 2. Init a method configuration

Use the annotation `@PostConstruct` to add your own custom initialization code to once the bean have been constructor.

```java
import jakarta.annotation.PostConstruct;
import org.springframework.stereotype.Component;
@Component
public class CricketCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15 minutes !!!";
    }
    @PostConstruct
    public void doMyStartupStuff() {
        System.out.println("In doMyStartupStuff(): " + getClass().getSimpleName());
    }
}
```

### 3. Destroy the method configuration

You can add the custom configuration of the destroy method by add your own custom logic into the method with the annotation `@PreDestroy` before the method.

```java
import jakarta.annotation.PostConstruct;
import jakarta.annotation.PreDestroy;
import org.springframework.stereotype.Component;
@Component
public class CricketCoach implements Coach {
    @Override
    public String getDailyWorkout() {
        return "Practice fast bowling for 15 minutes !!!";
    }
    @PostConstruct
    public void doMyStartupStuff() {
        System.out.println("In doMyStartupStuff(): " + getClass().getSimpleName());
    }
    @PreDestroy
    public void doCleanupStuff() {
        System.out.println("In doMyCleanupStuff(): " + getClass().getSimpleName());
    }
}
```

### 3. Prototype Beans and Destroy Lifecycle

There is a subtle point you need to be aware of with **prototype** scoped beans.

For **prototype** scoped beans, Spring does not call the destroy method.

In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean: the container instantiates, configures, and otherwise assembles a prototype object, and hands it to the client, with no further record of that prototype instance.

Thus, although initialization lifecycle callback methods are called on all objects regardless of scope, in the case of prototypes, configured destruction lifecycle callbacks are not called. The client code must clean up prototype-scoped objects and release expensive resources that the prototype bean(s) are holding.
