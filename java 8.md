### 1) **Java8 features**
**A. Lambda Expressions**

Lambda expressions allow you to write concise implementations of functional interfaces. 

Example: 

```java 

Copy code 

List<String> names = Arrays.asList("Alice", "Bob", "Charlie"); 
names.forEach(name -> System.out.println(name));
```

 

**B. Functional Interfaces**
Interface that contains exactly one abstract method is known as functional interface

Example: 

```java 
import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;
import java.util.function.Function;
import java.util.function.Consumer;

public class FunctionalExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        Predicate<Integer> isEven = n -> n % 2 == 0;
        Function<Integer, Integer> doubleIt = n -> n * 2;
        Consumer<Integer> printIt = n -> System.out.println("Processed: " + n);

        numbers.stream()
               .filter(isEven)            // Predicate
               .map(doubleIt)             // Function
               .forEach(printIt);         // Consumer
    }
}
//outpu
//Processed: 4
//Processed: 8
//Processed: 12

 ```

 

 **C. Streams API**

Streams provide a functional-style way to process collections of data. 

Example: 

```java 

Copy code 

List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David"); 
List<String> filteredNames = names.stream() 
                                  .filter(name -> name.startsWith("A")) 
                                  .collect(Collectors.toList()); 
System.out.println(filteredNames); // [Alice] 
 
```
 

 **D. Default and Static Methods in Interfaces**

Interfaces can now have methods with default or static implementations. 

Example: 

```java 


interface Vehicle { 
    default void start() { 
        System.out.println("Vehicle started"); 
    } 
    static void stop() { 
        System.out.println("Vehicle stopped"); 
    } 
} 
 
```
 

 **E. Optional**

The Optional class is a container that helps avoid NullPointerException. 

Example: 

```java 


Optional<String> name = Optional.ofNullable(null); 
System.out.println(name.orElse("Default Name")); // Default Name 

 ```

 **F. Method References**

Method references are a shorthand for lambda expressions. 

Example: 

```java 


List<String> names = Arrays.asList("Alice", "Bob", "Charlie"); 
names.forEach(System.out::println); // Method reference 
 ```

 

 **G. Collectors**

The Collectors class provides reduction operations for streams, such as grouping, joining, and averaging. 

Example: 

```java 


List<String> names = Arrays.asList("Alice", "Bob", "Charlie"); 
String joinedNames = names.stream().collect(Collectors.joining(", ")); 
System.out.println(joinedNames); // Alice, Bob, Charlie 
 ```

 **H. Parallel Streams**

Streams can be executed in parallel for faster processing on multi-core processors. 

Example: 

```java 

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5); 
int sum = numbers.parallelStream().reduce(0, Integer::sum); 
System.out.println(sum); // 15 
 
```
 

 **I. Base64 Encoding and Decoding**

The java.util.Base64 class provides Base64 encoding and decoding. 

Example: 

```java 

String encoded = Base64.getEncoder().encodeToString("Java8".getBytes()); 
System.out.println(encoded); // SmF2YTg= 
String decoded = new String(Base64.getDecoder().decode(encoded)); 
System.out.println(decoded); // Java8 
```
  **J. Flat Map**
  Solution 1
```java 
  public class Test {
    public static void main(String[] args) {
        List<List<Integer>> num = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4));
        num.stream().flatMap(Collection::stream).forEach(x -> System.out.print(x + " "));
    }
}
//output
//1 2 3 4
```
Solution 2
```java 
  public class Test {
    public static void main(String[] args) {
        List<List<Integer>> num = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4));
        num.stream().flatMap(Listn::stream).forEach(x -> System.out.print(x + " "));
    }
}
//output
//1 2 3 4
```
Solution 3
```java 
  public class Test {
    public static void main(String[] args) {
        List<List<Integer>> num = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4));
        num.stream().flatMap(list->list.stream).forEach(x -> System.out.print(x + " "));
    }
}
//output
//1 2 3 4
```
