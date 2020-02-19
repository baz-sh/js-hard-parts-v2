# Closure

## Closure Introduction

* Closure is the most esoteric of JavaScript concepts
* Enables powerful pro-level functions like 'once' and 'memoize'
* Many JavaScript design patterns including the mdoule pattern use closure
* Build iterators, handle partial application and maintain state in an asynchronous world

**Functions get a new memory every run/invocation**.

### Functions with memories

* When our functions get called, we create a live store of data (local memory/variable environment/state) for that functions execution context
* When the function finishes executiing, its local memory is deleted (except the returned value)
* But what if our functions could hold on to live data between exections?
* This would let out function definitions have an associated cache/persistent memory
* But it all starts with us **returning a function from another function.**

## Returning Functions

Functions can be returned from other functions in JavaScript.

```js
function createFunction() {
    function multiplyBy2 (num) {
        return num*2;
    }

    return multiplyBy2;
}

const generatedFunc = createFunction();
const result = generatedFunc(3); // 6
```

Internally, JS will process the following code in memory and assignment like below:

![returning-funcs](/img/03-returning-funcs.png)

## Nested Function Scope

You can call a function in the same function call it was defined.

```js
function outer() {
    let counter = 0;
    function incrementCounter() {
        counter++;
    }

    incrementCounter();
}

outer();
```

Here is a representation of what JS is doing under the hood with this code:

![nested](/img/03-nested.png)

## Retaining Function Memory

Calling a function outside of the function call in which it was defined.

```js
function outer() {
    let counter = 0;
    function incrementCounter() { counter++ }
    return incrementCounter;
}

const myNewFunction = outer();
myNewFunction();
myNewFunction();
```

The execution of this above code looks like below:

![sad-closure](/img/03-sad-closure.png)

When the function was "brought over" to the global memory, the data surrounding where the function was created was also brought over, like on a little backpack.

![closure-carry](/img/03-closure-carry.png)

## Function Closure

When `myNewFunction` is called and the increment counter is hit, it looks for the counter variable in it's local execution context. It doesn't exist so it looks up the chain, which is the function definition that lives in the global scope. As this was written with the counter in it's execution context _at the time it was created_, the counter variable exists as part of that function definition in the global scope.

![function-closure](/img/03-function-clouse-1.png)

The pointer that refers to myNewFunction is no longer just a function, but the data that's attached to it. This is what is meant by _closure_.

When we return the initial increment counter function, because of where it was declared, the surrounding variables are "closed over" and carried with it.

As long as the function definition is not overridden, then the data isn't in an exection contexts temporary memory, it's permanent on the global context from when the function was returned.

Note you cannot access this information. You're not allowed to say for example `myNewFunction.counter`.

What we can do with closure though in this example would be to have added logic to say something like "if counter == 1 then return, sorry you can't run me more than once.". Essentially it has permanent memory.

## Closure Technical Defnition Review

A fancy name for the "backpack" referred to in this course is the "closed over variable environment".

JavaScript has a very particular scope rule. It's called static or more commonly lexical scoping. That is to say, where I save my function determines for the rest of the life of that function what data, whenever it gets run, under whatever label it gets, what data it will have access to when that function runs. It's not where you run it (dynamic scoping).

Lexical scoping is the position of the data on the page. You control the scope when you write the code.

When the function was first run, we pulled the data out along with it on the lexically scoped property (counter).

**The rule is: Where my function was saved, determines what data I have access to, when its eventually run, whereever that may be.**

You can think of it as: Persistant Lexically Scoped Reference Data. AKA the "backpack" 😆

In the industry, we call this "Closure".

![backpack](/img/03-backpack.png)

## Multiple Closure Instances

## Practical Applications
