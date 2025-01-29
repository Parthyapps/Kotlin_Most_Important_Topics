# Kotlin Overview
- Kotlin is a **statically typed** programming language that runs on the **Java Virtual Machine (JVM)**.  
- Developed by **JetBrains**, it is widely used for **Android development** and other applications.  

# Kotlin Fundamentals
# 🚀 Key Features of Kotlin
## 1️⃣ Conciseness  
Kotlin reduces boilerplate code with type inference, smart casts, and data classes.  
## 2️⃣ Null Safety  
Eliminates NullPointerException by distinguishing between nullable and non-nullable types.  
## 3️⃣ Extension Functions  
Add new functions to existing classes without modifying their source code.  
## 4️⃣ Interoperability  
Fully compatible with Java, making migration seamless.  
## 5️⃣ Coroutines  
Simplifies asynchronous programming with lightweight, efficient threading.  
## 6️⃣ Data Classes  
Auto-generates `equals()`, `hashCode()`, `toString()`, and more for concise data modeling.  
## 7️⃣ Functional Programming  
Supports lambdas, higher-order functions, and immutable data structures.  
## 8️⃣ Smart Casts  
Automatically infers types, reducing explicit type checks.  
## 9️⃣ Ranges  
Provides a built-in range type for loops, conditions, and collections.  
## 🔟 Companion Objects  
Acts as a Kotlin alternative to static methods in Java, with class-level properties and functions.  

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

```kotlin
val name: String = "Kotlin"
var age: Int = 5
```
- Kotlin has various built-in data types such as String, Int, Double, and Boolean for storing different kinds of values.

# When 
- Explanation: A versatile conditional expression that can replace if-else chains.
  ```kotlin
  val result = when (x) {
    1 -> "One"
    2 -> "Two"
    else -> "Other" 
   }
  ```

# forEach
- Explanation: Iterates through each element in a collection.
- ``` listOf(1, 2, 3).forEach { println(it) } ```
  
# Data Classes and Collections
- Data classes are used to hold data. They automatically generate useful methods like toString(), equals(), and hashCode().

    ```kotlin  
      data class User(val name: String, val age: Int)
      val user1 = User("Alice", 30)
      println(user1) // Output: User(name=Alice, age=30)
     ```

# Collections
- Kotlin provides rich collection functions such as filter, map, and reduce for working with data.

# Filter 🎯: Select specific elements from a collection based on conditions.
   ```kotlin
     val numbers = listOf(1, 2, 3, 4, 5)
    val filtered = numbers.filter { it > 2 }
    println(filtered) // Output: [3, 4, 5]
   ```

# Reduce ➗: Aggregate a collection into a single value.
   ```kotlin
      val numbers = listOf(1, 2, 3, 4)  
      val sum = numbers.reduce { acc, num -> acc + num }  
      println(sum) // 10
   ```

# takeUnless ❌: Execute code unless a condition is true.
   ```kotlin
    val age = 20  
    val result = age.takeUnless { it < 18 } ?: "Underage"  
    println(result) // 20
   ```
re’s your Kotlin Scope Functions overview in Markdown (.md) format with concise key points:

# 🚀 Scope Functions in Kotlin  

Kotlin provides **scope functions** to simplify object operations. Here’s a quick guide:  
## 🔹 `let`  
✔ Used for **null checks** (`?.let { }`)  
✔ Executes block only if the object is **non-null**  

## 🔹 `apply`  
✔ Used for **object initialization**  
✔ Modifies properties and returns the **same object**  

## 🔹 `with`  
✔ Used when calling multiple functions on an object  
✔ **Does not return** the object but executes operations  

## 🔹 `run`  
✔ Combines **`let` + `with`**  
✔ Used for **initialization + computation**  
✔ Supports **null safety checks**  

## 🔹 `also`  
✔ Performs **extra operations** after initialization  
✔ Returns the **same object**  

# Kotlin: lateinit vs lazy – When to Use What?
-🔹 When to Use lateinit
- ✅ Used to initialize a variable later
- ✅ Ensure initialization before use
- ✅ Works only with var (mutable)
- ✅ Ideal when values change dynamically

- 🔹 When to Use lazy
- ✅ Initialization happens only when accessed
- ✅ Single initialization—cached value reused ♻️
- ✅ Works only with val (read-only)
- ✅ Best for heavy objects that depend on internal class values
  
# Extensions and Infix Functions
- ✅ Extension functions allow you to add new functionality to existing classes without altering their source code.
   ```kotlin
           val excited = "Hello".addExclamation()
           println(excited) // Output: Hello!
           fun String.addExclamation(): String {
             return this + "!"
           }
   ```
# Infix functions provide a way to call functions in a more natural language style, enhancing readability.
   ```kotlin
       infix fun Int.times(str: String) = str.repeat(this)
       val result = 2 times "Bye "
       println(result) // Output: Bye Bye 
   ```

# Inline
  - ✅ The inline keyword improves performance by avoiding function call overhead, especially for higher-order functions.
   ```kotlin
    fun main() {
        val result = calculate(5, 3) { x, y -> x + y }
        println("Result: $result") // Output: Result: 8
   }
    inline fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
        return operation(a, b)
     }
 ```
# Companion Object
- A companion object in Kotlin is an object declared inside a class that behaves like a static member in Java.
- Key Point: Every class can have at most one companion object.
- Companion Objects are tied to a class
- // Access without creating an instance
- Limit: A class can have only one companion object.
-         const val CONSTANT = "Static Value"
Why? The companion object is a way to provide static-like behavior in Kotlin, and Kotlin restricts it to one per class for simplicity and clarity.
Where to Use?

    To hold static functions or properties related to the class.
    For factory methods or constants associated with the class.

# Singleton Class
- A singleton class ensures that only one instance of the class is created throughout the application's lifecycle.
- Key Point: A singleton is a globally accessible instance.
- Limit: You can have as many singleton classes as you need in your application.
Why? Singleton classes are independent objects and are not tied to a specific class. They are useful whenever you need a single global instance of a class.
Where to Use?

    For managing globally shared resources like database connections, logging, or network clients.

# Emit
  - emit is a suspending function, meaning it must be called within a coroutine or another suspending function.
  - It’s often used inside a flow builder or any custom implementation where you generate a flow of data dynamically.

# Sealed Classes
- Sealed classes restrict class hierarchies to a limited set of subclasses, making them useful for representing state or results.
- Where to Use a Sealed Class

    Representing States:
        Example: Success, Error, Loading states in network calls.
    Handling Results:
        Example: Wrapping API responses with success or failure types.
    Modeling Finite Options:
        Example: User actions, navigation destinations, or specific operations.
    Event Handling in MVVM:
        Example: Events emitted from the ViewModel to the UI.
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
# Higher-Order Functions - Pass functions as a parameter or return them as function
Advantage:
- code Reusability
- Reducing Boilerplate Code:
- Better Performance: Inline functions reduce the runtime overhead by inlining the logic during compilation, which is critical for performance-sensitive Android apps.
- Flexibility
- Improved Readability:
 - Where to Use Higher-Order and Inline Functions in Android
 -      1.View Click Listeners: Use higher-order functions to handle repetitive UI tasks, such as click listeners or touch event listeners.
        2.Network Operations: Use higher-order functions to define common tasks like making API calls with callbacks.
        3.Custom RecyclerView Adapters: use higher-order functions to define item click or long-click listeners in RecyclerView.
        4.Utility Functions:  Define reusable higher-order functions for tasks like validating input, transforming data, or handling asynchronous operations.

```kotlin
fun main() {
    // Using the higher-order function for addition
    val additionResult = calculate(10, 20, ::add)
    println("Addition: $additionResult") // Output: 30

    // Using the higher-order function for subtraction
    val subtractionResult = calculate(10, 20) { a, b -> a - b }
    println("Subtraction: $subtractionResult") // Output: -10
}

// Higher-order function
fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

// Function for addition (function reference)
fun add(a: Int, b: Int): Int {
    return a + b
}
```
## Coroutines Features
- Coroutines are a Kotlin feature that allows you to write asynchronous, non-blocking code in a simple and readable way.
- coroutines are used to handle tasks like fetching data from the internet or reading from a database on a background thread.
- Coroutines are lightweight threads that allow us to execute concurrent code without blocking threads
- it's essential to avoid blocking the main thread
- A coroutine is a concurrency design pattern that you can use on Android to simplify code that executes asynchronously

Coroutines make asynchronous programming easier by allowing your code to run asynchronously while still being sequential and structured like synchronous code.
- Suspend Functions:
    - A suspend function is a special type of function that can suspend its execution and resume later. These functions are the building blocks of coroutines
- Coroutine Builders:
    - Coroutines in Kotlin are created using coroutine builders like launch, async, and runBlocking.
    - launch: Starts a new coroutine but does not return a result.
    - async: Starts a new coroutine and returns a result via a Deferred object, which can be awaited using await().
      - await():Suspends the execution of the current coroutine until the result of the Deferred is ready.This ensures that all API calls complete before combining the results.
    - runBlocking: Blocks the current thread until all coroutines inside the block have finished executing. This is mainly used in the main function or for testing.
- Dispatchers
   - Dispatchers define on which thread a coroutine will run.
   - Dispatchers.Main: Runs on the main thread, typically used for UI updates in Android.
   - Dispatchers.IO: Used for I/O operations (e.g., network calls, database operations).
   - Dispatchers.Default: Used for CPU-intensive tasks.
   - Dispatchers.Unconfined: Runs on the caller thread until suspension.

launch
  ```kotlin
          import kotlinx.coroutines.*
          fun main() {
            GlobalScope.launch { 
                delay(1000L) 
                println("Hello from Coroutine!")
            }
            println("Hello from Main Thread!")
            Thread.sleep(2000L)
          }
  ```
 - async is used when you need a result computed in a coroutine.
 ```kotlin
    import kotlinx.coroutines.*
    fun main() {
    GlobalScope.launch {
        val result = async { 
            computeResult() 
        }
        println("Computed result: ${result.await()}")
    }
    Thread.sleep(2000L)
    }
    suspend fun computeResult(): Int {
    delay(1000L)
    return 42
    }
 ```
- runBlocking is a bridge between non-coroutine world and coroutine world.
-  ```kotlin
   import kotlinx.coroutines.*

    fun main() = runBlocking { 
    launch { 
        delay(1000L) 
        println("Hello from Coroutine!")
    }
    println("Hello from Main Thread!")
    }
   In this code, we’re starting a main coroutine using runBlocking, and inside this coroutine, we're launching a new coroutine.
   
- Coroutine Context
- withcontext : Helps to switch between different coroutine dispatchers (e.g., from Dispatchers.IO to Dispatchers.Main). (Performing background tasks on Dispatchers.IO and updating the UI on Dispatchers.Main.)
- Every coroutine in Kotlin has a context associated with it, which is a set of various elements. The key elements in this set are Job of the coroutine and its dispatcher.
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
  
  - **Non-blocking:** Coroutines make it easy to perform long-running tasks without blocking the main thread.
  - **Structured concurrency:** Coroutines have a well-defined scope and lifecycle, which helps to avoid problems like leaks and orphaned coroutines. 
  - **Cancellation:** Coroutines can immediately cancel a request and free up resources.
  - **Performance:** Coroutines are lightweight and don't block threads.

## Coroutines scopes
- There are basically 3 scopes in Kotlin coroutines:
- 1.Global Scope - Not tied up with any lifecycle. Task run for entire app lifecycle until we cancel manually.( No lifecycle awareness, can lead to memory leaks or unmanaged resources.)
- 2.LifeCycle Scope. - Lifecycle aware and tied with Activity , fragment. coroutines are cancelled when activity reaches destory state.(Useful for UI-related tasks, such as animations, fetching data for the UI, or updating LiveData.)
- 3.ViewModel Scope - Lifecycle-aware scope tied to the ViewModel.Coroutines are automatically cancelled when the ViewModel is cleared.( Ideal for long-running tasks like API calls or database operations in ViewModel that survive configuration changes.)
- CoroutineScope: Fully customizable; used for independent tasks with manual control.
  

## Kotlin acesding order using for loops
``` kotlin
fun main(){
    val numbers = listOf(20, 18, 7, 10, 3, -12, 2, 1, -11, 15, -10, -5, -1, -19)
    val sortedNumbers = sortnumber(numbers)
    println(sortedNumbers)
}

fun sortnumber (numbers: List<Int>): List<Int>{
    val mutableNumbers = numbers.toMutableList()
    val n = mutableNumbers.size
    for (i in 0 until n -1 ){
       for (j in 0 until n - i - 1 ) {
           if (mutableNumbers[j] > mutableNumbers[j+1]){
               val temp = mutableNumbers[j]
              mutableNumbers[j] = mutableNumbers[j+1]
              mutableNumbers[j +1] = temp
           }
       }
    }
    return mutableNumbers
}

```
## Remove Vowel in the string
``` kotlin
fun main() {
   var string = "Welcome to Parthibhan!.."
    val result = removeVowels(string)
    println(result)
}
fun removeVowels(string: String): String{   
    val vowels = "aeiouAEIOU"
    return string.filter{
        char-> char !in vowels
    }
}
```
1.clean architechture
2.BroadCase
3.Room
4.Room Table how to migrate and not migrate 
5.flow koin
6.infix
7.solid principle
8.koin.
sealed class , enum classes


