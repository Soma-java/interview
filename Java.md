### 1) **String Buffer VS String Builder**
```java
public class StringPerformanceTest {
    public static void main(String[] args) {
        int iterations = 10000; // Append 1000 times

        // Measure time for StringBuffer
        long startTime = System.nanoTime();
        StringBuffer stringBuffer = new StringBuffer();
        for (int i = 0; i < iterations; i++) {
            stringBuffer.append("a");
        }
        long endTime = System.nanoTime();
        System.out.println("Time taken by StringBuffer: " + (endTime - startTime) / 1_000_000.0 + " ms");

        // Measure time for StringBuilder
        startTime = System.nanoTime();
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < iterations; i++) {
            stringBuilder.append("a");
        }
        endTime = System.nanoTime();
        System.out.println("Time taken by StringBuilder: " + (endTime - startTime) / 1_000_000.0 + " ms");
    }
}
//Output
Time taken by StringBuffer: 1.1574 ms
Time taken by StringBuilder: 1.0773 ms
```
