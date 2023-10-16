# JavaSE-Function

java.util.function.Function is a functional interface in Java that represents a function that takes one argument and produces a result. 

It's part of the Java Functional Interfaces introduced in Java 8 to support functional programming features.

Here's the basic structure of the Function interface:

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

T is the type of the input to the function.
R is the type of the result of the function.

The apply method takes an argument of type T and returns a result of type R.

Let's see an example to make it more concrete. Suppose you want to create a function that squares an integer:

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Define a Function that squares an integer
        Function<Integer, Integer> squareFunction = x -> x * x;

        // Use the apply method to get the result
        int result = squareFunction.apply(5);

        System.out.println("Square of 5: " + result);
    }
}
```

In this example:

We create a Function called squareFunction that takes an Integer as input and returns an Integer.

The lambda expression x -> x * x represents the function that squares its input.

We then use the apply method to apply the function to the value 5, resulting in the square of 5.

You can replace the types Integer with any other types you need, making it a versatile interface for various functional programming scenarios.

# More examples to illustrate the use of java.util.function.Function in different scenarios:

## Example 1: String Length

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function to get the length of a string
        Function<String, Integer> lengthFunction = s -> s.length();

        // Apply the function
        int length = lengthFunction.apply("Hello, World!");

        System.out.println("Length of the string: " + length);
    }
}
```

## Example 2: Convert String to Integer

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function to convert a String to Integer
        Function<String, Integer> convertToIntFunction = s -> Integer.parseInt(s);

        // Apply the function
        int result = convertToIntFunction.apply("123");

        System.out.println("Converted Integer: " + result);
    }
}
```

## Example 3: Composing Functions
```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function to square a number
        Function<Integer, Integer> squareFunction = x -> x * x;

        // Function to double the result
        Function<Integer, Integer> doubleFunction = x -> x * 2;

        // Compose the functions: square and then double
        Function<Integer, Integer> squareAndDouble = squareFunction.andThen(doubleFunction);

        // Apply the composed function
        int result = squareAndDouble.apply(5);

        System.out.println("Result after square and double: " + result);
    }
}
```

These examples demonstrate different use cases of the Function interface, from simple operations like getting the length of a string to more complex scenarios like composing multiple functions.

# More advance topics about "java.util.function.Function" in Java

The java.util.function.Function interface is a powerful tool, and there are some advanced topics and concepts you can explore:

## 1. Chaining Functions:

You can chain multiple functions together using the andThen and compose methods. andThen applies the current function first and then the next one, while compose applies the current function after the next one.

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        Function<Integer, Integer> add1 = x -> x + 1;
        Function<Integer, Integer> multiplyBy2 = x -> x * 2;

        // andThen: add 1 and then multiply by 2
        Function<Integer, Integer> add1AndMultiply = add1.andThen(multiplyBy2);
        int result1 = add1AndMultiply.apply(5); // (5 + 1) * 2 = 12

        // compose: multiply by 2 and then add 1
        Function<Integer, Integer> multiplyAndAdd1 = add1.compose(multiplyBy2);
        int result2 = multiplyAndAdd1.apply(5); // (5 * 2) + 1 = 11

        System.out.println("Result with andThen: " + result1);
        System.out.println("Result with compose: " + result2);
    }
}
```

## 2. Method References:
Java allows you to use method references to create functions concisely. If a method matches the functional interface's signature, you can refer to it by name.

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Using lambda expression
        Function<String, Integer> lengthFunction1 = s -> s.length();

        // Using method reference
        Function<String, Integer> lengthFunction2 = String::length;

        int result1 = lengthFunction1.apply("Hello"); // 5
        int result2 = lengthFunction2.apply("World"); // 5

        System.out.println("Result 1: " + result1);
        System.out.println("Result 2: " + result2);
    }
}
```

## 3. Custom Functional Interfaces:
You can create your own functional interfaces with custom input and output types. This allows you to define functions that suit your specific needs.

```java
@FunctionalInterface
interface MyFunction<T, U, R> {
    R apply(T t, U u);
}

public class FunctionExample {
    public static void main(String[] args) {
        MyFunction<Integer, String, String> customFunction = (i, s) -> i + " " + s;

        String result = customFunction.apply(42, "is the answer");
        System.out.println(result); // 42 is the answer
    }
}
```

## 4. Exception Handling:
You can handle exceptions within a Function using techniques like wrapping the function with a try-catch block or using a utility method.

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        Function<String, Integer> parseAndDouble = input -> {
            try {
                int parsedValue = Integer.parseInt(input);
                return parsedValue * 2;
            } catch (NumberFormatException e) {
                // Handle the exception, e.g., return a default value
                return -1;
            }
        };

        int result1 = parseAndDouble.apply("123"); // 246
        int result2 = parseAndDouble.apply("abc"); // -1

        System.out.println("Result 1: " + result1);
        System.out.println("Result 2: " + result2);
    }
}
```
