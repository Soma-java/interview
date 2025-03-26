 ## Table of Contents
1. [Status code and body validatio](#1-status-code-body)
2. [JSON Key-Value Pair Validation](#2-JSON-Key-Value-Pair-Validation)

### 1 **Status code and body validation**

Ans : 
```java
RestAssured.given()
                .baseUri("https://catfact.ninja")
                .get("/fact")
                .then()
                .statusCode(200)
                .body("length", equalTo(11));
```
### 2 **JSON Key-Value Pair Validation**
```java
response.then().body("key", equalTo("value"));
```
### 3 **Nested JSON Object Validation**
```java
response.then().body("parent.child.key", equalTo("value"));
```
### 4. **Array Validation**
```java
response.then().body("items.size()", equalTo(5)); // Check array size
response.then().body("items[0]", equalTo("value")); // Validate first item
```
### 5. **Status Code Validation**
```java
response.then().statusCode(200);
```
### 6. **Header Validation**
```java
response.then().header("Content-Type", equalTo("application/json"));
```
### 7. **Time Validation**
```java
response.then().time(lessThan(2000L)); // Response time should be less than 2 seconds
```
### 8. **Extracting Values**
**Extracting a Single Value**
```java
String value = response.then().extract().path("key");
```
**Extracting an Entire JSON Object**

```java
Map<String, Object> jsonObject = response.then().extract().as(Map.class);
```
to use above you have to use either GSON or JACKSON library
```pom
**GSON**
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version> <!-- Use the latest version -->
</dependency>
```
```pom
**JACKSON**
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.15.2</version> <!-- Use the latest version -->
</dependency>

```

### 9. **Validation Using Custom Matchers**
```java
response.then().body("key", containsString("partialValue"));
response.then().body("key", startsWith("prefix"));

```
### 10. **Cookie Validation**
**Specific Cookie**
```java
1.response.then().cookie("sessionId", equalTo("abc123"));

2.String sessionId = response.then().extract().cookie("sessionId");
```
**All Cookies**
```java
Map<String, String> cookies = response.then().extract().cookies();
```
