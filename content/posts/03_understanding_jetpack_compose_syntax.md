+++ title = "Helping you understand the syntax of Jetpack Compose"  
date = "2021-01-02"  
author = "Oussama Hafferssas"  
cover ="/img/00_the_blog_s_readme/cover_site_readme.svg"  
description = "In this article, I will demessify the syntax of Jetpack Compose for you by using pure Kotlin, interactive code that you can read and modify, and what you already know about OOP. I'll explain some of the frequently used fancy words when using Compose."  
+++


>*[Edit history](https://github.com/hfrsoussama/oussamahaff_dev/commits/master/content/posts/00_the_blog_s_readme.md) of this post can be found in the blog's Github repository.*



I believe that if you are reading this article you already know that
Jetpack Compose is a new Kotlin framework which enables you to build UIs
for Android applications, and also for Kotlin desktop applications.

However, Jetpack Compose brings a syntax that may look strange for some
of us - developers - especially those doing mainly Object-Oriented
Programming.

Therefore, in this article I’ll try to demessify the syntax of Jetpack
Compose by using basic and pure Kotlin, interactive code that you can
read and modify, and what you already know about OOP. Along the path,
you may get impressed also by the simplicity that hides behind some of
the fancy words used to explain Jetpack Compose.

[TOC levels=1-3]: #

# Table of Contents
- [Basic Jetpack Compose Syntax](#basic-jetpack-compose-syntax)
- [From OOP to Function Composition](#from-oop-to-function-composition)
  - [Basic OOP](#basic-oop)
  - [Getting to Top-Level !](#getting-to-top-level-)
  - [Changing your point of view !](#changing-your-point-of-view-)
  - [Going Higher-Order !](#going-higher-order-)
  - [Invoking the function parameter](#invoking-the-function-parameter)
  - [Being Anonymous !](#being-anonymous-)
  - [Trailing Lambda](#trailing-lambda)
  - [The one last thing to do !](#the-one-last-thing-to-do-)
- [The Final Result](#the-final-result)



# Basic Jetpack Compose Syntax
This is how the syntax of Jetpack Compose looks like in general. At the
end of the article, we will compare it with our code that we will be
refactoring in a step-by-step guide.

{{< figure
src="/img/03_understanding_jetpack_compose_syntax/compose-syntax.jpg"
position="center" style="border-radius: 8px;"  
caption="*Kotlin* syntax used for *Jetpack Compose* to show an Image"  
captionPosition="center" >}}


# From OOP to Function Composition

## Basic OOP
Let's say we want to print the result of the multiplication of two
floats. By using the classical approach of Object-Oriented Programming,
we can write something like this in Kotlin :

> *You can **run** the source code to test it*

{{< playground embeded_link="https://pl.kotl.in/Jo5cBRoEk?from=1&to=25&readOnly=false&theme=darcula" embeded_height="55"/>}}

> *This Kotlin code can get more compact, but we will keep it as*
> ***explicit** as it could be for the sake of clarity.*

The three lines of code in the `main()` function represent the usual
three basic steps that we generally use in Object-Oriented Programming
- Instantiating an object
- Tell the object to do the work by invoking one if its methods
- Present the result to the user


Now, let's find out a way to implement the same functionality but by
writing the code differently.

## Getting to Top-Level !
- First, we will add a function that multiplies two parameters. But we
  will place it outside of any class.
- Instead of giving it a verb as a name like `multiply`, we will give it
  a ***noun*** as a name like `multiplication`.

{{< playground
embeded_link="https://pl.kotl.in/eoAb7djBJ?from=1&to=19&readOnly=false&theme=darcula"
embeded_height="50" />}}

By putting a function outside any class or interface in Kotlin, we are
making it a ***top-level function***. We can understand why it's called
***top-level*** just by rotating the editor's canvas.

{{< figure
src="/img/03_understanding_jetpack_compose_syntax/top_level.jpg"
position="center" style="border-radius: 8px;"  
caption="Why it's called ***top-level*** function"  
captionPosition="center" >}}



Let's do the same for the function that prints the result.
- Declare a new printing function as a **top-level** function
- Give it a **noun name**. Let's call it `prettyPrinter`.

Our code will look like the part in `// The new style`

{{< playground
embeded_link="https://pl.kotl.in/90jJR36l9?from=1&to=22&readOnly=false&theme=darcula"
embeded_height="50" />}}

> *You can run the program to verify that we still have the same result*
> *that will print to the user*.


## Changing your point of view !

Let's say that we don't want to use an intermediate variable to store
the result of multiplication. In our example, this means deleting the
use of the variable `multiplicationResult`.  
There are **two ways** to do it.

**The first**, which is classical OOP and you may already guessed it, is by
deleting it from `prettyPrinter` function and replacing it by a call
(invokation) of the function `multiplicationResult` inside of the
*String* message like this


{{< playground
embeded_link="https://pl.kotl.in/iXGv60DsV?from=1&to=22&readOnly=false&theme=darcula"
embeded_height="50" />}}

It's true that the program will give the same result, but unfortunately
it has nothing to with Jetpack Compose syntax that we are looking for.

Note also that the function `prettyPrinter` now ***prints exclusively***
the result of the function `multiplication` and not any `Float` given to
it. Which makes the function `prettyPrinter` not reusable at all !

Let's try **the second** way of doing things.



By going back to our code we had this :

```kotlin
    // The new style
    val multiplicationResult = multiplication(paramY = 4f, paramX = 5f)
    prettyPrinter(result = multiplicationResult)
```

Now, before deleting the variable `multiplicationResult`, we will play
with its type.

The actual type `multiplicationResult` is `Float`, which is the type
returned by the function `multiplication`. Therefore, we can write this
:
```kotlin
    // The new style
    val multiplicationResult: Float = multiplication(paramY = 4f, paramX = 5f)
    prettyPrinter(result = multiplicationResult)
```


Please **look** at `multiplicationResult` declaration.

The declaration means that you represent **the result of the
invokation** of the function `multiplication` by a variable.

What about the **representation of the function** by itself ? Is there a
way to declare it ?

Fortunately, the answer is yes, and this is how it looks like :
```kotlin
    // The new style
    val operation: ()-> Float = { multiplication(paramY = 4f, paramX = 5f) }
```
You can read it as follows :
- On the left side : the variable `operation` is of type `()-> Float`
  which means that it's of type ***function that does something and
  return Float***.
- On the tight side : ***what this function does*** is represented by what's
  inside `{ }`. In our case, it does multiplication and returns a Float.

Now, lets refactor our code to use this new function representation.


## Going Higher-Order !

Our function `prettyPrint` was a simple function accepting a `Float` as
a parameter like this

```kotlin
fun prettyPrinter(result: Float) {
    println("The result is : $result")
}
```
In order to pass the new representation of our `multiplication` function
as parameter, we need to refactor our function like this :
```kotlin
fun prettyPrinter(operationAsParam: ()-> Float) {
    println("The result is : $operationAsParam")
}
```
Note that :
- We changed the name of the parameter to `operationAsParam` just for clarification
- The type of the parameter has changed from `Float` to `()-> Float`

Our program will look like this after refactoring :

{{< playground
embeded_link="https://pl.kotl.in/TOEJP1D30?from=1&to=22&readOnly=false&theme=darcula"
embeded_height="50" />}}

> *I'll explain later why the result of multiplication is not displayed*
> 😉

By doing this refactoring, a *fancy* expression can be used to describe
the function `prettyPrinter`
>we can say : ***prettyPrinter is Higher-Order Function***

Which simply means that it **accepts a function as a parameter**.



However, the goal is not to show you only Kotlin features. So, we will
keep going on with our refactoring.


## Invoking the function parameter
If you run the program where we have left, you will get this result :
`Function0<java.lang.Float>` instead of printing the result of the
multiplication (in our case `20.0`).

This is simply because we are trying to print the *representation of the
function* by using directly the name of the parameter in
`$operationAsParam` instead of the value returned after invoking
(running) the function.

To fix this, you just need to modify the String template from this
representation of the function :

```kotlin
    println("The result is : $operationAsParam")
```

to an invocation by adding `()` after the name of the parameter :

```kotlin
    println("The result is : ${operationAsParam()}")
```

This will actually replace the function parameter name with the value
returned by the function after its invocation.

> Feel free to modify the interactive code to test it by yourself 🙂


## Being Anonymous !
Thanks to our last factoring, we can now delete the intermediate
variable called `operation`

```kotlin
    val operation: ()-> Float = { multiplication(paramY = 4f, paramX = 5f) }
    prettyPrinter(operationAsParam = operation)
```

to obtain this :

```kotlin
    prettyPrinter(operationAsParam = { multiplication(paramY = 4f, paramX = 5f) } )
```

We can simplify it by deleting the non-essential named parameter like
this :

```kotlin
    prettyPrinter( { multiplication(paramY = 4f, paramX = 5f) } )
```

Now we don't have any intermediate variable 👌 and our code will run
like a charm !

{{< playground
embeded_link="https://pl.kotl.in/jg4r0qxOs?from=1&to=11&readOnly=false&theme=darcula"
embeded_height="30" />}}

Let me explain something here, by deleting the intermediate variable, we
deleted what identifies our function `{ multiplication(paramY = 4f,
paramX = 5f) }`. Therefore, in programming we call it an ***Anonymous
Function*** !

In Kotlin, when we have a *higher-order function* (in our case
`prettyPrinter`) which has only one parameter passed as an anonymous
function expression (like in our case) we can delete the parenthesis and
write this :

```kotlin
    prettyPrinter { multiplication(paramY = 4f, paramX = 5f) } 
    // or
    prettyPrinter { 
        multiplication(paramY = 4f, paramX = 5f) 
    } 
```

> Feel free to modify the interactive code to test it by yourself 😉

By doing this, we can say that we have achieved a syntax that actually
looks the syntax of Jetpack Compose just by combining functions.

In programming this is called
[***function composition***](https://en.wikipedia.org/wiki/Function_composition_(computer_science)).
I guess you know now why it's called Compose 😉

## Trailing Lambda
We will add a small thing to our code to make it more Compose-alike.

Actually, the function `prettyPrinter` prints a fixed message with the
result which is not really flexible. To avoid this, we will pass it as a
parameter like this :

```kotlin
    fun prettyPrinter(message: String, operationAsParam: ()-> Float) {
        println("$message ${operationAsParam()}")
    }
```

By doing this, we need to pass its value when calling the function like
this :

{{< playground
embeded_link="https://pl.kotl.in/5yoy74kVN?from=1&to=11&readOnly=false&theme=darcula"
embeded_height="30" />}}

By now you can ask : why we write on parameter inside the
parenthesis (The `message` parameter) while the function has two
parameters ?

The answer is that this is a convention Kotlin. Because the last
parameter of () is a function, when calling it we can write the
expression of the function parameter outside the parenthesis.

This convention is called
[***Trailing Lambda***](https://kotlinlang.org/docs/reference/lambdas.html#passing-a-lambda-to-the-last-parameter).



## The one last thing to do !

- Just capitalize the names of the two functions to get
  `PrettyPrinter(...` and `Multiplication(...`
- Give the `message` parameter a default value to avoid writing it when
  calling the function each time.

You are done now, Bravo !

You can check the final code bellow and test the result

{{< playground
embeded_link="https://pl.kotl.in/RgQbx4Nwy?from=1&to=21&readOnly=false&theme=darcula"
embeded_height="50" />}}



# The Final Result
As you can see, the final representation using only functions (*function
composition*) gives as the same result given by the OOP style.

This is the mindset that you will need when reading or writing UI code
with Jetpack Compose, it's all about functions !

{{< juxtaposer
label_1="Jetpack Compose"
src_1="/img/03_understanding_jetpack_compose_syntax/compose-syntax.jpg"  
label_2="Pure Kotlin"
src_2="/img/03_understanding_jetpack_compose_syntax/pure-kotlin-functions.jpg" />}}

*I hope Thanks you for taking the time to read this article* : )

> [*Comment*](https://github.com/hfrsoussama/oussamahaff_dev/issues/new/choose)
> *using Github issues to avoid cross-site trackers.*


Written by [Oussama Hafferssas](https://twitter.com/OussamaHaff). Thanks to [***NAME FAMILLY-NAME***](https://twitter.com/----) for
reviewing the content.
