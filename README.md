# Kotlin Overview
Kotlin is a statically typed programming language that runs on the Java Virtual Machine (JVM).
It was developed by JetBrains, the same company behind IntelliJ IDEA, Kotlin's preferred IDE.
Kotlin is a modern programming language that is used primarily for Android development but has broader applications as well. 
If you're looking to master Kotlin, here’s a structured overview of the key topics, from basics to more advanced concepts:

# Kotlin Oops concepts 
- OOP stands for Object-Oriented Programming.

Procedural programming is about writing procedures or methods that perform operations on the data, while object-oriented programming is about creating objects that contain both data and methods.

Object-oriented programming has several advantages over procedural programming:

    OOP is faster and easier to execute
    OOP provides a clear structure for the programs
    OOP helps to keep the Kotlin code DRY "Don't Repeat Yourself", and makes the code easier to maintain, modify and debug
    OOP makes it possible to create full reusable applications with less code and shorter development time

1.Class and Object
    Concept: A class is a blueprint for creating objects, and an object is an instance of a class.
    Object:  represents the real-life entities, which have states and behavior
2.Inheritance
    Concept: A class can inherit properties and methods from another class (parent class).
3.Encapsulation
    Concept: Restricting direct access to class properties and methods, typically using access modifiers.
4.Abstraction
    Concept: Hiding implementation details and exposing only the necessary functionality through abstract classes or interfaces.

# Kotlin Fundamentals
- **1.Conciseness**: Kotlin reduces boilerplate code compared to Java. It achieves this through features like type inference, smart casts, data classes, and more.
- **2.Null Safety**: Kotlin's type system distinguishes between nullable and non-nullable types, helping to eliminate the dreaded NullPointerException. You must explicitly specify when a variable can hold a null value.
- **3.Extension Functions**: Kotlin allows you to add new functions to existing classes without modifying their source code. This feature enhances code readability and reusability.
- **4.Interoperability**: Kotlin is fully interoperable with Java. You can use Kotlin code in existing Java projects and vice versa, which makes adoption easier, especially in legacy codebases.
- **5.Coroutines**: Kotlin provides first-class support for coroutines, which are lightweight threads that help manage asynchronous code. Coroutines simplify complex asynchronous programming tasks, making code more readable and maintainable.
- **6.Data Classes**: Kotlin's data classes automatically generate equals(), hashCode(), toString(), copy(), and componentN() methods based on properties defined in the primary constructor. This feature is especially useful for modeling immutable data.
- **7.Functional Programming**: Kotlin supports functional programming paradigms, including higher-order functions, lambdas, and immutable data structures. These features enable concise and expressive code.
- **8.Smart Casts**: Kotlin's compiler performs automatic type casts when certain conditions are met. This feature eliminates the need for explicit type checks and casts in many situations, leading to cleaner code.
- **9.Ranges**: Kotlin provides a built-in range type that represents a sequence of numbers. Ranges are commonly used in loops, conditions, and collections to express a range of values concisely.
- **10.Companion Objects**: Kotlin allows you to define a companion object within a class, which is similar to static methods and fields in Java. Companion objects can access private members of their enclosing class and serve as a replacement for static utility classes.

# Basic Syntax and Fundamentals
- Variables and Constants: Understanding **var (mutable) and val (immutable)** for declaring variables.
- Data Types: Familiarity with basic types such as **Int, Double, String, Boolean**, and their usage.
- Control Flow: Mastery of **if, when, for, while, and do-while** statements for controlling the program flow.
 ```kotlin
          val number = 10
        if (number > 5) {
            println("Greater than 5")
        } else {
            println("Less than or equal to 5")
        }
        when (number) {
            1 -> println("One")
            2 -> println("Two")
            in 3..10 -> println("Between 3 and 10")
            else -> println("Greater than 10")
        }
```
- Scope of a variable – A variable exists only inside the block of code( {………….} ) where it has been declared. You can not access the variable outside the loop. Same variable can be declared inside the nested loop – so if a function contains an argument x and we declare a new variable x inside the same loop, then x inside the loop is different than the argument. Naming Convention – Every variable should be named using lowerCamelCase.

```kotlin
val name: String = "Kotlin"
var age: Int = 5
```
- Kotlin has various built-in data types such as String, Int, Double, and Boolean for storing different kinds of values.
# Data Classes and Collections
- Data classes are used to hold data. They automatically generate useful methods like toString(), equals(), and hashCode().

```kotlin  
  data class User(val name: String, val age: Int)
  val user1 = User("Alice", 30)
  println(user1) // Output: User(name=Alice, age=30)
 ```
# Collections
- Kotlin provides rich collection functions such as filter, map, and reduce for working with data.

```kotlin
 val numbers = listOf(1, 2, 3, 4, 5)
val filtered = numbers.filter { it > 2 }
println(filtered) // Output: [3, 4, 5]
```
# Extensions and Infix Functions
- Extension functions allow you to add new functionality to existing classes without altering their source code.
```kotlin
  fun String.addExclamation(): String {
    return this + "!"
}
val excited = "Hello".addExclamation()
println(excited) // Output: Hello!
```
- Infix functions provide a way to call functions in a more natural language style, enhancing readability.
```kotlin
  infix fun Int.times(str: String) = str.repeat(this)
  val result = 2 times "Bye "
  println(result) // Output: Bye Bye 
```
# Sealed Classes
- Sealed classes restrict class hierarchies to a limited set of subclasses, making them useful for representing state or results.
  ```kotlin
  sealed class Result {
    data class Success(val data: String) : Result()
    data class Failure(val error: String) : Result()
  }
  fun fetchData(): Result {
      return Result.Success("Data fetched successfully")
  }
  when (val result = fetchData()) {
      is Result.Success -> println(result.data)
      is Result.Failure -> println(result.error)
  }
  ```
# Higher-Order Functions
Reusability: The processStudents function can be reused with different filtering and transformation logic.
Readability: The code becomes more readable and expressive, as the logic is encapsulated within well-defined functions.
Functional Programming: This approach aligns with functional programming principles, allowing for concise and clear code.

```kotlin
fun main() {
    val passingStudents = processStudents(
        students,
        { student -> student.grade >= 70 }, // Filter: grades >= 70
        { student -> "${student.name} (${student.grade})" } // Transform: "Name (Grade)"
    )
    println("Passing Students: $passingStudents")
}
```
# Coroutines in Kotlin
- Coroutines are a Kotlin feature that allows you to write asynchronous, non-blocking code in a simple and readable way.
- Kotlin coroutines provide a higher-level abstraction for managing background tasks without the complexities of threads or callbacks.
- coroutines are used to handle tasks like fetching data from the internet or reading from a database on a background thread. By using Dispatchers.Main for UI updates and Dispatchers.IO for network calls, you can ensure that your app is responsive and performs well.
- Why Use Coroutines?
  
In traditional asynchronous programming, you use threads, callbacks, or frameworks like RxJava to perform tasks asynchronously. However, these approaches can lead to:

    Callback Hell: When callbacks are deeply nested.
    Complex Code: Managing multiple threads can be challenging and error-prone.

Coroutines make asynchronous programming easier by allowing your code to run asynchronously while still being sequential and structured like synchronous code.
- Suspend Functions:
    A suspend function is a special type of function that can suspend its execution and resume later. These functions are the building blocks of coroutines
- Coroutine Builders:
    Coroutines in Kotlin are created using coroutine builders like launch, async, and runBlocking.
    launch: Starts a new coroutine but does not return a result.
    async: Starts a new coroutine and returns a result via a Deferred object, which can be awaited using await().
    runBlocking: Blocks the current thread until all coroutines inside the block have finished executing. This is mainly used in the main function or for testing.
- Dispatchers
   Dispatchers define on which thread a coroutine will run.
   Dispatchers.Main: Runs on the main thread, typically used for UI updates in Android.
   Dispatchers.IO: Used for I/O operations (e.g., network calls, database operations).
   Dispatchers.Default: Used for CPU-intensive tasks.
   Dispatchers.Unconfined: Runs on the caller thread until suspension.
- Job
   A Job represents a coroutine and allows you to manage its lifecycle (e.g., start, cancel, wait for completion).
   You can cancel a Job to stop the coroutine.
  ```kotlin
  fun main() = runBlocking {
    val job = launch {
        repeat(1000) { i ->
            println("Coroutine working: $i")
            delay(500L)
        }
    }
    delay(1300L)
    println("Main: I'm tired of waiting!")
    job.cancel() // Cancels the coroutine
    println("Main: Job is cancelled.")
  }
  Coroutine working: 0
  Coroutine working: 1
  Coroutine working: 2
  Main: I'm tired of waiting!
  Main: Job is cancelled.
  ```
# Advantages of Coroutines
 **Non-blocking:** Coroutines make it easy to perform long-running tasks without blocking the main thread.
 **Structured concurrency:** Coroutines have a well-defined scope and lifecycle, which helps to avoid problems like leaks and orphaned coroutines. 
 **Cancellation:** Coroutines can immediately cancel a request and free up resources.
 **Performance:** Coroutines are lightweight and don't block threads.


