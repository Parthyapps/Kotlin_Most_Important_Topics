# Kotlin Overview
- Kotlin is a **statically typed** programming language that runs on the **Java Virtual Machine (JVM)**.  
- Developed by **JetBrains**, it is widely used for **Android development** and other applications.
- Built-in Null Safety. Safe calls (?.), Elvis operator (?:), and non-null assertion (!!) help handle nulls safely.
- NullPointException (NPE) is a common runtime issue
- safe call (?.) can hold a null value 
- DSL Support - Natural DSL via lambdas/context receivers
- Multiplatform - KMM supports Android, iOS, Web
- Data Class - A data class is a special class in Kotlin designed to hold data (state)
- while automatically generating useful methods like: toString(),equals() & hashCode(),copy()

## 1️⃣ Safe Call Operator (?.)
- Used to safely access a property or method only if the variable is not null.

      val name: String? = null
      val length = name?.length  // returns null instead of throwing NPE
## 2️⃣ Elvis Operator (?:)
- Used to provide a default value if the expression on the left is null.

      val name: String? = null
      val finalName = name ?: "Guest"
## 3️⃣ Not-Null Assertion Operator (!!)
- “Trust me, I know this value is not null. Let me use it without extra checks.”
- ⚠️ Only use !! when you're absolutely sure the variable is not null — otherwise it's dangerous.

      val name: String? = null
      val length = name!!.length // ❌ This will throw NPE

# Kotlin Fundamentals
Exceptions: Understanding try-catch blocks, throwing exceptions, and creating custom exceptions.
Sealed Classes: Using sealed classes for representing restricted class hierarchies, often used in error handling.

# Val & Const
- var is a mutable variable — you can reassign values.
- val - (value) is a read-only variable that can be initialized at runtime.
- val cannot be reassigned
  
            **- val recyclerView: RecyclerView = findViewById(R.id.recycler_view)**
- const val is Compile-Time Constant (Like static final in Java) and can only be used with top-level or object classes, not inside functions or regular classes.
- Use const for global constants (like API keys, mathematical constants, or configuration values) that never change.
- Inside an object or companion object:

         object AppConfig {
                const val BASE_URL = "https://api.example.com"
                const val MAX_RETRY = 3
            }

# Kotlin: lateinit vs lazy – When to Use What?
-🔹 When to Use lateinit both lateinit and lazy used for defer property initialization.
- **Use lateinit when we dont know the initial value at the time class creation.**
- ✅ Can be used with var (mutable)
- ✅ lateinit cannot used with nullabale types
- ✅ Works with non primitive data types only
- ✅ lateinit cannot be used with primitive type (Int, char, float)
-     lateinit var binding: ActivityMainBinding 

- 🔹 When to Use lazy
- initilize the property only when its accessed for the first time.
- ✅ Can be used with only val (immutable)
- ✅ Delays initialization until used	
- ✅ lazy properties are checked for initialization at compile time.
- ✅ lazy can be used with primitive type (Int, char, float)
- ✅ for constant variable use lazy and value not change
- Initialization happens only when accessed, not before.
```kotlin
  val retrofit by lazy {
    Retrofit.Builder()
        .baseUrl("https://api.example.com")
        .build()
  }
 ```
# kotlin Delegates:
- Kotlin provides property delegates to move logic outside the property itself using the by keyword.
- Built-in delegates like lazy, observable, and notNull improve performance and state tracking.
- lazy - Lazy Initialization, observable - Property Change Listener, vetoable - Conditionally Accept Change.

# 🚀 Scope Functions in Kotlin  
Kotlin provides **scope functions** to simplify object operations. Here’s a quick guide:  
## 🔹 `let`  Object Reference : it, Return Value: Lambda result
✔ Used for **null checks** (`?.let { }`)  
✔ Executes block only if the object is **non-null**  
```kotlin
fun main(){  
   var name : String? = "Kotlin let check"
   name?.let { println(it) } //prints Kotlin let null check
   name = null
   name?.let { println(it) } // nothing will print

   liveData.observe(viewLifecycleOwner, Observer { data ->
       data?.let { nonNullData ->
           // Process non-null data
           updateUI(nonNullData)
       }
   })
}
```
## 🔹 `apply`  Object Reference : this, Return Value: Context object
✔ Used for **object initialization**  
✔ Modifies the **object** and **returns the same object**.
   ```kotlin
      data class Student (var name: String = "", var age: Int=0)
      fun main(){
          val student = Student().apply{
              name = "parthi"
              age = 23
          }
          println(student)
      }
  ```

## 🔹 `also`  Object Reference : it, Return Value: Context object
✔ Used for performing additional actions on an object
✔ Returns the **same object**  
```kotlin
      val list = mutableListOf(1, 2, 3)
      list.also {
          it.add(4)
          Log.d("ListDebug", "List after adding: $it")
      }
```
## 🔹 `with`  Object Reference : this, Return Value: Lambda result
✔ Used for grouping operations on an object.
✔ **Does not return** the object but executes operations  
```kotlin
      val recyclerView = findViewById<RecyclerView>(R.id.recyclerView)
      with(recyclerView) {
          layoutManager = LinearLayoutManager(context)
          adapter = NewsAdapter(newsList)
          setHasFixedSize(true)
      }
```

## 🔹 `run`  Object Reference : this, Return Value: Lambda result
✔ Combines **`let` + `with`**  
✔ Used for object configuration and returning a result.
✔ Use run when you need to perform multiple operations and return a result.
✔ Supports **null safety checks**  
```kotlin
val userName = getSharedPreferences("MyPrefs", MODE_PRIVATE).run {
    getString("USER_NAME", "Guest")
}
textView.text = "Hello, $userName"

val result = run {
    val a = 10
    val b = 20
    a + b // Returns the result of the lambda
}
println("Result: $result") // Output: Result: 30
```
# Higher-Order Functions 
- Pass functions as a parameter or return them as function
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

# Extensions and Infix Functions
- ✅ Extension functions allow you to add new functionality to existing classes without altering their source code.
   ```kotlin
           val excited = "Hello".addExclamation()
           println(excited) // Output: Hello!
           fun String.addExclamation(): String {
             return this + "!"
           }

             // Add an extension function to View to show a toast
          fun View.showToast(message: String, duration: Int = Toast.LENGTH_SHORT) {
              Toast.makeText(context, message, duration).show()
          }
          
          // Usage in an Activity
          button.setOnClickListener {
              it.showToast("Button clicked!")
          }
   ```
# Infix 
- Allows calling a function without . and parentheses () (like operators).
  An infix function allows you to call a function in an infix notation (i.e., without using a dot . or parentheses ()).
   ```kotlin
   // Define an infix function
        fun main() {
         val result = 5 add 10 // Infix notation
          println(result) // Output: 15
        }
         infix fun Int.add(value: Int): Int {
          return this + value
          }         
   ```

# Inline
  - Inline function is instruct compiler to insert the complete body of the function wherever that fun get used in the code.
  - Adv: Function call overhead doesn't occur.Less overhead and faster program excution.
  - The inline keyword tells Kotlin to copy the function body directly where it's called (instead of creating a function object).
  - Helps in performance optimization when using lambdas.
  - When func code is very small good idea to make inline
  - When fun code is large and called from so many places dont use inline, large code will be repeat again and again

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
- Declared inside a class, behaves like a static member in Java.
- Key Point: Only one companion object per class.
- Tied to a class, accessible without creating an instance.
- Used for static functions, properties, factory methods, or constants.
- Example: `const val CONSTANT = "Static Value"`

# Singleton Class
- A singleton is a design pattern that ensures only one instance of a class is created and provides a global access point to that instance.
- Key Point: Globally accessible instance.
- No limit on the number of singleton classes in an application.
- Used for managing shared resources like database connections, logging, or network clients.

# Emit
- emit is used in Kotlin Flow to emit values asynchronously in a coroutine.
- Dynamically generates a flow of data.
- Commonly used in custom flow implementations.

# Sealed Classes
It’s useful when working with state management or representing different types of results.
- ✔ Restricts inheritance (only subclasses in the same file)
- Useful for representing states, results, or finite options.
- Example: Success, Error, Loading states in network calls.
- Example Code:
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

## Coroutines Features
- Coroutines are a Kotlin feature that allows you to write asynchronous, non-blocking code in a simple and readable way.
- coroutines are used to handle tasks like fetching data from the internet or reading from a database on a background thread.
- Coroutines are lightweight threads that allow us to execute concurrent code without blocking threads
- it's essential to avoid blocking the main thread
- A coroutine is a concurrency design pattern that you can use on Android to simplify code that executes asynchronously

Coroutines make asynchronous programming easier by allowing your code to run asynchronously while still being sequential and structured like synchronous code.
- **Suspend Functions:**
    - A suspend function is a special type of function that can suspend its execution and resume later. These functions are the building blocks of coroutines
- ✅ **Coroutine Builders**:
    - Coroutines in Kotlin are created using coroutine builders like launch, async, and runBlocking.
    - ✅ launch: Starts a new coroutine but does not return a result.
    - ✅ async: Starts a new coroutine and returns a result via a Deferred object, which can be awaited using await().
      - await():Suspends the execution of the current coroutine until the result of the Deferred is ready.This ensures that all API calls complete before combining the results.
    - ✅ runBlocking: Blocks the current thread until all coroutines inside the block have finished executing. This is mainly used in the main function or for testing.
    - ✅ withcontext(Dispatchers.IO) - switches to a different thread.
      
- ✅ **Dispatchers**
   - Dispatchers define on which thread a coroutine will run.
   - Dispatchers.Main: Runs on the main thread, typically used for UI updates in Android.
   - Dispatchers.IO: Used for I/O operations (e.g., network calls, database operations).
   - Dispatchers.Default: Used for CPU-intensive tasks.
   - Dispatchers.Unconfined: Runs on the caller thread until suspension.

✅ 1. Synchronous API call (sequential execution)
-Here, both API calls run one after the other — synchronously (sequentially).

    lifecycleScope.launch {
        val userResponse = apiService.getUser() // waits until this finishes
        val postsResponse = apiService.getPosts() // starts after userResponse is done
        
        if (userResponse.isSuccessful && postsResponse.isSuccessful) {
            // handle data
        }
    }

✅ 2. Asynchronous (concurrent) API call using async
- Use async to run them in parallel, both kick off immediately, and wait for results when you need them.
- This saves time because both calls are executed in parallel, and only wait when you call .await().

       lifecycleScope.launch {
            val userDeferred = async { apiService.getUser() }
            val postsDeferred = async { apiService.getPosts() }
        
            val userResponse = userDeferred.await()
            val postsResponse = postsDeferred.await()
        
            if (userResponse.isSuccessful && postsResponse.isSuccessful) {
                // Both responses are ready now
            }
        }

  ✅ 3. Run parallel calls in background (IO Dispatcher)

      CoroutineScope(Dispatchers.IO).launch {
        val userDeferred = async { apiService.getUser() }
        val postsDeferred = async { apiService.getPosts() }
    
        val user = userDeferred.await()
        val posts = postsDeferred.await()
    
        // process data
    }

- **Coroutine Context**
- ✅ **withcontext **: Helps to **switch between different coroutine dispatchers** (e.g., from Dispatchers.IO to Dispatchers.Main). (Performing background tasks on Dispatchers.IO and updating the UI on Dispatchers.Main.)
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
- ✅ 1.Global Scope - Not tied up with any lifecycle. Task run for entire app lifecycle until we cancel manually.( No lifecycle awareness, can lead to memory leaks or unmanaged resources.)
- ✅ 2.LifeCycle Scope. - Lifecycle aware and tied with Activity , fragment. coroutines are cancelled when activity reaches destory state.(Useful for UI-related tasks, such as animations, fetching data for the UI, or updating LiveData.)
- ✅ 3.ViewModel Scope - Lifecycle-aware scope tied to the ViewModel.Coroutines are automatically cancelled when the ViewModel is cleared.( Ideal for long-running tasks like API calls or database operations in ViewModel that survive configuration changes.)
- ✅ CoroutineScope: Fully customizable; used for independent tasks with manual control.
- ✅ CoroutineScope -> Cancel whenever any of its children fail.
- ✅ SupervisorScope -> If we want to continue with the other tasks even when one fails, we go with the supervisorScope. A supervisorScope won’t cancel other children when one of them fails.

## Delays & Timeouts
- delay(1000l) - pause coroutine without blocking
- withTimeout(5000L) - cancels if execution exceeds time
- yield - allows other coroutines to run before resuming

## Error handling
- try {} catch {} - standard exception handling
- supervisorscope - ensure child coroutine fails indepently
- coroutineExceptionHandler - handles uncaught exception

# 🚀 Key Features of Kotlin
## 1️⃣ Conciseness - Kotlin reduces boilerplate code with type inference, smart casts, and data classes.  
## 2️⃣ Null Safety - Nullable Types: Understanding the concept of nullability and using safe calls (?.), the Elvis operator (?:), and the non-null assertion operator (!!).
## 3️⃣ Extension Functions - Add new functions to existing classes without modifying their source code.  
## 4️⃣ Interoperability - Fully compatible with Java, making migration seamless.  
## 5️⃣ Coroutines - Simplifies asynchronous programming with lightweight, efficient threading.  
## 6️⃣ Data Classes - Auto-generates `equals()`, `hashCode()`, `toString()`, and more for concise data modeling.  
## 7️⃣ Functional Programming - Supports lambdas, higher-order functions, and immutable data structures.  
## 8️⃣ Smart Casts - Automatically infers types, reducing explicit type checks.  
## 9️⃣ Ranges - Provides a built-in range type for loops, conditions, and collections.  
## 🔟 Companion Objects - Acts as a Kotlin alternative to static methods in Java, with class-level properties and functions.  
## improved Multiplatform Support
Now fully stable — Write once, run on JVM, JS, iOS, Linux, etc.
## Error Handling

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
