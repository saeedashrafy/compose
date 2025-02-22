### What are Scope functions?
## Scope functions are functions in the Kotlin standard library whose purpose is to execute a block of code within the context of an object. It provides a temporary scope when you call the function on the object with a lambda expression. In this scope, the function can access the object without its name. There are five scope functions

- let
- run
- with
- apply
- also

## How do they refer to the context object?
## Inside the lambda of a scope function, the context object could be referenced in 2 ways

## as a lambda receiver (this)
## lambda argument (it)

![](https://github.com/saeedashrafy/learn/blob/main/Screenshot%201403-12-05%20at%2007.08.51.png)


## let
## Context object: it
### Returns: Result of the lambda expression
### Use case: Perform operations on a nullable object, transformation, chaining functions.
 
```
@kotlin.internal.InlineOnly
public inline fun <T, R> T.let(block: (T) -> R): R {
    contract {
        callsInPlace(block, InvocationKind.EXACTLY_ONCE)
    }
    return block(this)
}

```

```
val somethingObject = SomethingFactory.getSomething()
  somethingObject?.let { something ->
      println("Hello, $it") 
  }

if(something != null) {
}
```

## apply
## Context object: this
### Returns: The same object (useful for builder-style modifications)
### Use case: Configure an object.

```
@kotlin.internal.InlineOnly
public inline fun <T> T.apply(block: T.() -> Unit): T {
    contract {
        callsInPlace(block, InvocationKind.EXACTLY_ONCE)
    }
    block()
    return this
}

class Person {
  var name: String = ""
  var age: Int = 0
}

val person = Person().apply {
  name = "Jeremy"
  age = 31
  println("Updated age: $age")
}
```
## also
## Context object: it
### Returns: The same object
### Use case: Perform additional actions (like logging/debugging).

```
val numbers = mutableListOf(1, 2, 3).also {
    println("Initial list: $it")
}
```

## with
## Context object: this
### Returns: Result of the lambda expression
### Use case: Work with an object without modifying it.

```
val person = Person("Alice", 25)
val introduction = with(person) {
    "Hi, I'm $name and I'm $age years old."
}
println(introduction)
```

## run
## Context object: this
### Returns: Result of the lambda expression
### Use case: Execute a block of code and return the result.

```
val person = Person("John", 30)
val bio = person.run {
    "My name is $name and I am $age years old."
}
println(bio)
```
