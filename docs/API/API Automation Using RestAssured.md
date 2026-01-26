---
sidebar_position: 12
---

## API Automation using RestAssured (Java)

RestAssured is a **Java-based API automation library** widely used with **TestNG and Cucumber**.
It integrates seamlessly with **Maven, TestNG, and CI pipelines**, making it the industry standard for API automation in Java projects.
This document shows **how RestAssured fits with both TestNG and Cucumber (Given–When–Then)** using **practical code examples**.

---

## Why RestAssured?

- Java-friendly DSL
- Easy request/response validation
- Strong JSON support
- Works well with TestNG & Maven
- Ideal for CI execution

RestAssured is **code-first automation**, unlike Postman.

---

## Prerequisites

- Java basics
- Maven project
- Understanding of REST & HTTP
- JSON fundamentals

---

## Maven Dependencies

```xml
<dependency>
  <groupId>io.rest-assured</groupId>
  <artifactId>rest-assured</artifactId>
  <version>5.4.0</version>
  <scope>test</scope>
</dependency>
```

(Optional)
```xml
<dependency>
  <groupId>org.hamcrest</groupId>
  <artifactId>hamcrest</artifactId>
  <version>2.2</version>
  <scope>test</scope>
</dependency>
```

---

## Basic RestAssured Structure

```java
given()
    .baseUri("https://api.example.com")
    .header("Authorization", "Bearer token")
.when()
    .get("/users/101")
.then()
    .statusCode(200);
```

Flow:
```
given → when → then
```

---

## GET Request Example

```java
given()
    .queryParam("status", "ACTIVE")
.when()
    .get("/users")
.then()
    .statusCode(200)
    .body("size()", greaterThan(0));
```

---

## POST Request Example

```java
given()
    .contentType("application/json")
    .body(payload)
.when()
    .post("/users")
.then()
    .statusCode(201);
```

Tester tip:
> Always validate **side effects**, not just status.

---

## Handling Headers & Params

```java
given()
    .header("Authorization", "Bearer " + token)
    .pathParam("id", 101)
.when()
    .get("/users/{id}");
```

---

## JSON Validation

```java
.then()
    .body("id", equalTo(101))
    .body("email", notNullValue());
```

Avoid:
- Full JSON comparison
- Fixed array index unless required

---

## Extracting Values from Response

```java
int userId =
given()
.when()
    .post("/users")
.then()
    .extract()
    .path("id");
```

Used for:
- API chaining
- End-to-end flows

---

## Logging (Debugging)

```java
given()
    .log().all()
.when()
    .get("/users")
.then()
    .log().all();
```

Best practice:
- Enable logging on failure
- Avoid logging sensitive data

---

## Authentication Handling

- Fetch token once
- Store securely
- Reuse across tests

Example:
```java
String token = getAuthToken();
```

---

# Example PART 1️⃣ RestAssured with TestNG

## Basic GET API Test

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

import org.testng.annotations.Test;

public class GetUserTest {

    @Test
    public void getUserDetails() {

        given()
            .baseUri("https://api.example.com")
            .header("Authorization", "Bearer " + TokenUtil.getToken())
        .when()
            .get("/users/101")
        .then()
            .statusCode(200)
            .body("id", equalTo(101))
            .body("email", notNullValue());
    }
}
```

---

## POST API Test with TestNG

```java
@Test
public void createUser() {

    String payload = "{ "name": "John", "email": "john@gmail.com" }";

    int userId =
    given()
        .contentType("application/json")
        .body(payload)
    .when()
        .post("/users")
    .then()
        .statusCode(201)
        .extract()
        .path("id");
}
```

---

# Example PART 2️⃣ RestAssured with Cucumber (BDD)

## Feature File

```gherkin
Feature: User API

  Scenario: Fetch user details
    Given user API is available
    When I fetch user with id 101
    Then response status should be 200
    And user email should be present
```

---

## Step Definitions

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

import io.cucumber.java.en.*;

public class UserSteps {

    private io.restassured.response.Response response;

    @Given("user API is available")
    public void apiAvailable() {
        baseURI = "https://api.example.com";
    }

    @When("I fetch user with id {int}")
    public void fetchUser(int id) {
        response =
        given()
            .header("Authorization", "Bearer " + TokenUtil.getToken())
        .when()
            .get("/users/" + id);
    }

    @Then("response status should be {int}")
    public void validateStatus(int status) {
        response.then().statusCode(status);
    }

    @Then("user email should be present")
    public void validateEmail() {
        response.then().body("email", notNullValue());
    }
}
```

---

## TestNG vs Cucumber

| Aspect | TestNG | Cucumber |
|---|---|---|
| Style | Code-first | BDD |
| Speed | Faster | Slower |
| Use case | Regression | Acceptance |

---

## Common Automation Mistakes ❌

- Hardcoding URLs
- Hardcoding tokens
- Ignoring response time
- Not validating DB side effects
- Mixing test logic & setup logic

---

## Best Practices ✅

- Use BaseTest for common setup
- Externalize environment config
- Keep tests independent
- Validate only what matters
- Clean up test data
- Use TestNG for core API automation
- Use Cucumber when BDD is required
- Centralize auth & config
- Validate DB side effects

---

## Interview-Ready Questions

**Q: Why RestAssured over Postman?**  
A: RestAssured enables code-based automation, CI execution, and better control.

**Q: What is given–when–then?**  
A: A BDD-style structure for readable API tests.

---

## Key Takeaways 🎯

- RestAssured is core API automation tool
- Integrates with Maven & TestNG
- Supports clean assertions
- Ideal for CI pipelines
- Strong complement to DB validation
- RestAssured works with TestNG & Cucumber
- Same API logic reused
- Choose framework based on project needs