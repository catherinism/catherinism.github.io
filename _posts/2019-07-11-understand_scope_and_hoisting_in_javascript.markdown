---
layout: post
title:      "Understand Scope & Hoisting in JavaScript"
date:       2019-07-11 19:08:44 -0400
permalink:  understand_scope_and_hoisting_in_javascript
---


If you're new to JavaScript, you might have encountered *scope* and *hoisting* and wondered what they are about or how they work.  It is important to learn these concepts as they will benefit you as you learn more about JavaScript, or once you start building JS applications. In this article, we will take a look at these two concepts and understand how *variables* affect them. 

But what are *variables*? Like in many programming languages, *variables* are containers for storing data values. These data values can be any data types like *strings*, *numbers*, or *objects*, and they can also be later reassigned or modified. The keywords to declare a value are `var`, `let`, and `const`. To declare a value, you need to assign it a name. 

For example:

`var valueName = "John"`

In this example, we assigned the *string* `"John"` to the `valueName` using the *variable* keyword `var`. If you don't use any of the 3 *variable* keywords, the *variable* will have a global scope.

`var` is the only keyword that was used to declare a *variable* before ES6. Take a look at the table below to better understand the differences between `var`, `let`, and `const`. This will give you a good grasp of how *hoisting* and *scope* work.

| Keywords | Scope| Hoisted | Redeclared | Reassigned |
| -------- | -------- | -------- | -------- |
| var   | function | ✔   | ✔   | ✔   |
| let   | block |   |   | ✔   |
| const   | block |   |    |    |    |


**SCOPE**

*Scope* dictates a portion of a program where a particular *variable* is accessible or visible. 

**SCOPE TYPES**

***Global Scope*** - *variables* declared outside of a *block {}* are accessible across the program. And as mentioned above, if you don't use any of the 3 *variable* keywords, the *variable* will have a global scope. This is something that developers are told to avoid.


```
var valueName = "John"
// code here can use valueName

function scope() {
// code here can use valueName even if it was declared outside this function
}
```

Another example but is not recommended.

```
scope();

function scope() {
 valueName = "John" // valueName can be accesssed everywhere because a variable keyword wasn't used. 
}
```

***Local Scope*** - *variables* declared inside of a block

```
// code here can not use valueName

function scope() {
   var valueName = "John"
   // code here can use valueName
}
```

**LOCAL SCOPE SUBTYPES**


**Function Scope** - *variables* inside the function are only accessible within the function

```
function scope() {
   var valueName = "John"
   console.log(valueName)
}

scope() // this will return John because it was printed(console.log) inside the function
```


**But** when you try to print it outside the *scope*:

```
function scope() {
   var valueName = "John"
}

scope() // undefined
console.log(valueName) // Reference error: "valueName is not defined"
```


**Block Scope** - variables defined inside a block {} using *let* or *const*  cannot be accessed outside that block while  *var* can be accessed outside of that block

```
function scope() {

  if (true) {
    var valueName = "John" // function scope
    let valueJob = "Teacher" // block scope    
    const valueAge = 30 // block scope

    console.log(valueName)
    console.log(valueJob) 
    console.log(valueAge)
  }
}

scope() // since the values were printed inside the block, the values below will be returned

John
Teacher
30
```

What do you think will be the result if they're printed outside the block?

```
function scope() {
  if (true) {
    var valueName = "John" // function scope
    let valueJob = "Teacher" // block scope    
    const valueAge = 30 // block scope
  }
	
   console.log(valueName)
   console.log(valueJob)
   console.log(valueAge)
}

scope() 
John // the only value returned because valueName has a function scope. The others will get a reference error(not defined)
```

**HOISTING**

*Hoisting* is when the variable or function declarations are hoisted or moved to the top. Remember that *hoisting* only happens with *function declaration*, not *function expression*. During the compilation process, the *variable* and *function declarations* are put into memory, then later get interpreted.

![](http://i68.tinypic.com/14tomxl.png)

This is how I imagine how hoisting looks like; and inside the container are declarations that can be hoisted:)

Simple Example:

```
valueName("John") // called before valueName(name) function was declared

function valueName(name) {
  console.log("My name is " + name)
}
```

The result will be *"My name is John"* because `valueName(name)` was hoisted to the top. Although *hoisting* doesn't move any of your code physically, it still looks as if:

```
function valueName(name) {
  console.log("My name is " + name)
}

valueName("John")
```

**NOT HOISTED**

*  *variables* declared with `let` and `const`

```
valueName() // ReferenceError: Cannot access 'varName' before initialization

const valueName = function() {
   console.log("John")
}
```

*  initializations

```
console.log(valueName) // undefined
var valueName = "John"
```

Only the *variable* declaration `var valueName` was hoisted but not the initialization `valueName = "John"`

*  function expressions

```
valueName() // TypeError: expression is not a function

var valueName = function() {
   console.log("John")
}
```

Only the *variable* declaration `var valueName` was hoisted but not the assignment of the *function* to `valueName`.

For some reason, knowing what cannot be moved to the top helped me comprehend more how *hoisting* works.


I hope this brief explanation somehow cleared up any confusion you may have regarding JavaScript's *scope* and *hoisting*. Happy coding!
