## Table of Contents
1. [Gson-POJO](#1-Goson-pojo)
2. [Jackson Data -POJO](#2-Jackson-Data-POJO)
 ### 1. **GSON-POJO**
  ```java
  package org.example;

import com.google.gson.Gson;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.testng.annotations.Test;
import org.example.entity.Object;

public class AppTest {

    @Test
    public void getAPI() {
        RestAssured.baseURI = "https://api.restful-api.dev/objects";
        Response response = RestAssured.given().get("/1");
        Gson gson = new Gson();
        Object object = gson.fromJson(response.getBody().asString(), Object.class);
        System.out.println(object.getName());
    }
}

Output :
  Google Pixel 6 Pro
  ```
```java
  package org.example.entity;

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
  
   ### 2. **Jackson-POJO**
```java
package org.example;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.example.entity.MyObject;
import org.testng.annotations.Test;

public class AppTest {

    @Test
    public void getAPI() throws JsonProcessingException {
        RestAssured.baseURI = "https://api.restful-api.dev/objects";
        Response response = RestAssured.given().get("/1");
        ObjectMapper mapper = new ObjectMapper();
        MyObject object = mapper.readValue(response.getBody().asString(), MyObject.class);
        System.out.println(object);
        System.out.println(object.getName());
    }
}
output :
MyObject{id='1', name='Google Pixel 6 Pro', data=Data{color='Cloudy White', capacity='128 GB'}}
Google Pixel 6 Pro
```
```java
package org.example.entity;

public class MyObject {
    private String id;
    private String name;
    private Data data;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

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

    @Override
    public String toString() {
        return "MyObject{" +
                "id='" + id + '\'' +
                ", name='" + name + '\'' +
                ", data=" + data +
                '}';
    }
}

```
```java
package org.example.entity;

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

    @Override
    public String toString() {
        return "Data{" +
                "color='" + color + '\'' +
                ", capacity='" + capacity + '\'' +
                '}';
    }
}

```
