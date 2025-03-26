 ## Table of Contents
1. [String-payload](#1-String-payload)
2. [Map-payload and Jackson Data Library](#2-Map-payload-JacksonDataLibrary)
3. [Map-payload and GSON Library](#3-Map-payload-GSONLibrary)
4. [Java Object Payload](#4-Java-Object-Payloadd)
5. [Java-Priority](#5-Java-Priority)

### 1. **String Payload**
Maven library
https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind

```java
package org.example;

import io.restassured.RestAssured;
import io.restassured.response.Response;
import io.restassured.specification.RequestSpecification;

public class AppTest {
    @org.testng.annotations.Test
    public void test() {
        String body = "{\n" +
                "   \"name\": \"mac\",\n" +
                "   \"data\": {\n" +
                "      \"year\": 2025,\n" +
                "      \"price\": 2000.99,\n" +
                "      \"CPU model\": \"apple chip\",\n" +
                "      \"Hard disk size\": \"128 GB\"\n" +
                "   }\n" +
                "}";
        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(body)
                .header("Content-Type", "application/json")
                .post("/objects");


        System.out.println("Status code:" + response.getStatusCode());
        System.out.println("response :"+response.getBody().asPrettyString());
        System.out.println("response time :"+response.getTime());
        String contentType = response.getContentType();
        System.out.println("Contetent type :"+contentType);
    }

}

output :

Status code:200
response :{
    "id": "ff808181932badb60195d1ac0ae73dfb",
    "name": "mac",
    "createdAt": "2025-03-26T08:57:48.007+00:00",
    "data": {
        "year": 2025,
        "price": 2000.99,
        "CPU model": "apple chip",
        "Hard disk size": "128 GB"
    }
}
response time :939
Contetent type :application/json

```
### 2. **Map-paload and Jackson Data Library**
```java
package org.example;

import com.fasterxml.jackson.core.JsonProcessingException;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import com.fasterxml.jackson.databind.ObjectMapper;

import java.util.HashMap;
import java.util.Map;

public class AppTest {
    @org.testng.annotations.Test
    public void test() throws JsonProcessingException {
        Map<String, Object> dataMap = new HashMap<>();
        dataMap.put("year", 2025);
        dataMap.put("price", 2000.99);
        dataMap.put("CPU_model", "apple chip");
        dataMap.put("Hard_disk_size", "128 GB");

        // Creating main map
        Map<String, Object> bodyMap = new HashMap<>();
        bodyMap.put("name", "mac");
        bodyMap.put("data", dataMap);

        ObjectMapper objectMapper = new ObjectMapper();
        String jsonBody = objectMapper.writeValueAsString(bodyMap);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");


        System.out.println("Status code:" + response.getStatusCode());
        System.out.println("response :" + response.getBody().asPrettyString());
        System.out.println("response time :" + response.getTime());
        String contentType = response.getContentType();
        System.out.println("Contetent type :" + contentType);
    }

}

output

Status code:200
response :{
    "id": "ff808181932badb60195d1bd9ef53e28",
    "name": "mac",
    "createdAt": "2025-03-26T09:17:00.021+00:00",
    "data": {
        "year": 2025,
        "price": 2000.99,
        "CPU_model": "apple chip",
        "Hard_disk_size": "128 GB"
    }
}
response time :957
Contetent type :application/json

```
### 3. **Map-payload and GSON Library**
```java
package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;

import java.util.HashMap;
import java.util.Map;

public class AppTest {
    @org.testng.annotations.Test
    public void test() {
        Map<String, Object> dataMap = new HashMap<>();
        dataMap.put("year", 2025);
        dataMap.put("price", 2000.99);
        dataMap.put("CPU_model", "apple chip");
        dataMap.put("Hard_disk_size", "128 GB");

        // Creating main map
        Map<String, Object> bodyMap = new HashMap<>();
        bodyMap.put("name", "mac");
        bodyMap.put("data", dataMap);

        //GSON
        Gson gson = new Gson();
        String jsonBody = gson.toJson(bodyMap);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");


        System.out.println("Status code:" + response.getStatusCode());
        System.out.println("response :" + response.getBody().asPrettyString());
        System.out.println("response time :" + response.getTime());
        String contentType = response.getContentType();
        System.out.println("Contetent type :" + contentType);
    }

}
output:


Status code:200
response :{
    "id": "ff808181932badb60195d1c3276c3e3e",
    "name": "mac",
    "createdAt": "2025-03-26T09:23:02.636+00:00",
    "data": {
        "year": 2025,
        "price": 2000.99,
        "CPU_model": "apple chip",
        "Hard_disk_size": "128 GB"
    }
}
response time :845
Contetent type :application/json
```

### 4. **Java Object Payload**
Data Class
```java
public class Data {
    private String color;
    private String capacity;

    public String getColor() {
        return color;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public String getCapacity() {
        return capacity;
    }

    public void setCapacity(String capacity) {
        this.capacity = capacity;
    }
}
```
Object class
```java
package org.example.entity;

public class Object {
    private String name;
    private Data data;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Data getData() {
        return data;
    }

    public void setData(Data data) {
        this.data = data;
    }
}

```
main class
```java
package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.example.entity.Data;
import org.example.entity.Object;

public class AppTest {
    @org.testng.annotations.Test
    public void test() {
        Object object = new Object();
        Data data = new Data();
        data.setColor("red");
        data.setCapacity("100 GB");
        object.setName("raj");
        object.setData(data);

        //GSON
        Gson gson = new Gson();
        String jsonBody = gson.toJson(object);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");


        System.out.println("Status code:" + response.getStatusCode());
        System.out.println("response :" + response.getBody().asPrettyString());
        System.out.println("response time :" + response.getTime());
        String contentType = response.getContentType();
        System.out.println("Contetent type :" + contentType);
    }

}

output:

Status code:200
response :{
    "id": "ff808181932badb60195d1c9995f3e4a",
    "name": "raj",
    "createdAt": "2025-03-26T09:30:05.023+00:00",
    "data": {
        "color": "red",
        "capacity": "100 GB"
    }
}
response time :847
Contetent type :application/json
```
### 5. **Java Priority**
```java
package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.example.entity.Data;
import org.example.entity.Object;
import org.testng.annotations.Test;

public class AppTest {
    private String id;

    //    @Test(priority = 2)
    @Test(dependsOnMethods = "postRequest")
    public void getAPI() {
        RestAssured.baseURI = "https://api.restful-api.dev/objects";
        Response response = RestAssured.given().get("/" + id);
        System.out.println(response.getBody().asPrettyString());
    }

    @Test()
    public void postRequest() {
        Object object = new Object();
        Data data = new Data();
        data.setColor("red");
        data.setCapacity("100 GB");
        object.setName("raj");
        object.setData(data);

        //GSON
        Gson gson = new Gson();
        String jsonBody = gson.toJson(object);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");
        String id = response.jsonPath().getString("id");
        System.out.println("Id :" + id);
        this.id = id;
    }

}
output :

Id :ff808181932badb60195d1de92f63ea0
{
    "id": "ff808181932badb60195d1de92f63ea0",
    "name": "raj",
    "data": {
        "color": "red",
        "capacity": "100 GB"
    }
}
```
### 6. **TestNG Priority**
Method 1 : dependsOnMethods
```java
package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.example.entity.Data;
import org.example.entity.Object;
import org.testng.annotations.Test;

public class AppTest {
    private String id;

    @Test(dependsOnMethods = "postRequest")
    public void getAPI() {
        RestAssured.baseURI = "https://api.restful-api.dev/objects";
        Response response = RestAssured.given().get("/" + id);
        System.out.println(response.getBody().asPrettyString());
    }

    @Test()
    public void postRequest() {
        Object object = new Object();
        Data data = new Data();
        data.setColor("red");
        data.setCapacity("100 GB");
        object.setName("raj");
        object.setData(data);

        //GSON
        Gson gson = new Gson();
        String jsonBody = gson.toJson(object);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");
        String id = response.jsonPath().getString("id");
        System.out.println("Id :" + id);
        this.id = id;
    }

}
```
Method 2 : TestNG priority
```java
package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.example.entity.Data;
import org.example.entity.Object;
import org.testng.annotations.Test;

public class AppTest {
    private String id;

    @Test(priority = 2)
    public void getAPI() {
        RestAssured.baseURI = "https://api.restful-api.dev/objects";
        Response response = RestAssured.given().get("/" + id);
        System.out.println(response.getBody().asPrettyString());
    }

    @Test(priority = 1)
    public void postRequest() {
        Object object = new Object();
        Data data = new Data();
        data.setColor("red");
        data.setCapacity("100 GB");
        object.setName("raj");
        object.setData(data);

        //GSON
        Gson gson = new Gson();
        String jsonBody = gson.toJson(object);

        RestAssured.baseURI = "https://api.restful-api.dev";
        Response response = RestAssured.given()
                .body(jsonBody)
                .header("Content-Type", "application/json")
                .post("/objects");
        String id = response.jsonPath().getString("id");
        System.out.println("Id :" + id);
        this.id = id;
    }

}

```
