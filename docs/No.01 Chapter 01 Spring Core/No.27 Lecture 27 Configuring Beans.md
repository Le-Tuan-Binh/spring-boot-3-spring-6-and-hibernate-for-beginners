## Configuring Beans

### 1. Development Process

- Create `@Configuration` class
- Define `@Bean` method to configure the bean
- Inject the bean into our controller

**Step 1: Create the Java Class and Annotation as `Configuration`**

```java
@Configuration
public class SportConfig {
    
}
```

This is basiclly a configuration class for configuring Spring using our custom approach.

**Step 2: Define `@Bean` method to configure the bean**

```java
@Configuration
public class SportConfig {
    @Bean
    public Coach swimCoach() {
        return new SwimCoach();
    }
}
```

We also can modify the Bean Id like the code below

```java
@Configuration
public class SportConfig {
    @Bean("aquatic")
    public Coach swimCoach() {
        return new SwimCoach();
    }
}
```

Now when in the controller you can see use the id `aquatic`.

**Step 3: Inject the bean into our controller**

```java
@RestController
public class CoachController {
    private Coach coach;
    @Autowired
    public CoachController(@Qualifier("swimCoach") Coach coach) {
        this.coach = coach;
    }
    @GetMapping("/dailyworkout")
    public String getDailyWorkout() {
        return coach.getDailyWorkout();
    }
}
```

We are inject the bean using the bean id, we use the `@Qualifier` annotation to use of the bean id.

### 2. Use case for the annotation `@Bean`

You may wonder that, Using `new` keyword is that it??? Why not just annotate the class with `@Component`.

The main usecase for `@Bean` Annotation is

- Make an existing third-party class available to Spring Framework.

- You may not have access to the source code of third-party class

- However, you would like to use the third-party class as a Spring Bean.

### 3. Real World Project Best Practices

In the real world, our projects used Amazon Web Service (AWS) to store the documents

- Amazon Simple Storage Service (Amazon S3)

- Amazon S3 is a cloud-based storage system for storing. It can store PDF documents, images, etc...

Now we wanted to use the AWS S3 client as a Spring Bean in our application.

The AWS S3 client code is a part of AWS SDK, we can't modify the AWS SDK source code and we can't just add `@Component`. However we can configure as a Spring bean using `@Bean`.

### 3. Configure AWS S3 Client using `@Bean`

So here is some sample codes similar to the project that i have worked on.

```java
@Configuration
public class DocumentsConfig {
    @Bean
    public S3Client remoteClient() {
        ProfileCredentialsProvider credentialsProvider = ProfileCredentialsProvider.create();
        Region region = Region.US_EAST_1;
        S3Client s3Client = S3Client.builder()
                .region(region)
                .credentialsProvider(credentialsProvider)
                .build();
        return s3Client;
    }
}
```

So in this, it is return to the Spring Bean so we can use in the other parts of our Spring Application.

### 4. Inject the S3Client as a bean

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;
import software.amazon.awssdk.services.s3.S3Client;

@Component
public class DocumentsService {

    private S3Client s3Client;

    @Autowired
    public DocumentsService(S3Client s3Client) {
        this.s3Client = s3Client;
    }

}
```

### 5. Store our document in S3

```java
@Component
public class DocumentsService {
    private S3Client s3Client;
    @Autowired
    public DocumentsService(S3Client s3Client) {
        this.s3Client = s3Client;
    }
    public void processDocument(Document document) {
        PutObjectRequest putObjectRequest = PutObjectRequest.builder()
                .bucket(bucketName)
                .key(subDirectory + "/" + fileName)
                .acl(ObjectCannedACL.BUCKET_OWNER_FULL_CONTROL).build();
        s3Client.putObject(putObjectRequest, RequestBody.fromInputStream(fileInputStream, contentLength));
    }

}
```

### 6. Wrap Up

We could use the Amazon S3 Client in our Spring application, the Amazon S3 Client was not originally annotated with `@Component`.

However, we configured the S3 Client as a Spring Bean using `@Bean`. It is now a Spring Bean and we can inject into other service of out application.

Make an existing third-party class available to Spring Framework.