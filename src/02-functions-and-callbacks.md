# Functions & Callbacks

The core premis of function is writing code once and then reusing it again and again with different values / data.

## Generalized Functions

'Parameters' (_placeholders_) mean we don't need to decide what data to run our functionality on until we run the function. Then we can provide an acutal value (_argument_) when we run the function.

Higher order functions follow this same principle. We may not want to decide exactly what some of our functionality is until we run our function.

## Repeating Functionality

Overview of exection context when using a function that uses an array for an argument.

![repeating](/img/02-repeating.png)

## Higher Order Functions

Often we write code that does somethiing, often to find out that we want to change it ever so slightly. Example looping over an array and multiplying the number or dividing it etc.

![hof-repeating](/img/02-hof-repeating.png)

There is a better way to handle this scenario. We can pass in part of the functionality. This is what's known as 'Higher Order Functions'.

![hof-short](/img/02-hof-short.png)

## Higher Order Functions Example

Here we are passing our function and instruction on what to do, this itself is a function. This means each of these functions have their own execution context and memory assignment. The execution is also maintained by the callstack.

![hof](/img/02-hof-1.png)

![hof-2](/img/02-hof-2.png)

## Callbacks & Higher Order Functions

Functions in JavaScript are first class objects. This is to say tehy can co-exist with and can be treated like any other javaScript object.

1. Assigned to variables and properties of other objects
2. Passed as arguments into functions
3. Returned as values from functions

**Higher-order functions** takes in—or passes out—a function. It's also just a term to describe these functions. Any function that does it we call that. There's nothing different about them inherently.

**Callbacks and Higher Order Functions simplify our code and keep it DRY**.

_Declarative readable code:_ Map, filter, reduce—the most readable way to write code to work with data

_Codesmith & pro interview prep:_ One of the most popular topics to test in interview both for Codesmith and mod/senio level job interviews

_Asynchronous JavaScript:_ Callbacks are a core aspect of async JavaScript, and are under-the-hood of promises, async/await

## Arrow Functions

Arrow functions are a short hand way to save functions.

They can be written such:

![arrow](/img/02-arrow.png)

Arrow functions also have their own execution context:

![arrow-2](/img/02-arrow-execution.png)

The arrow function in the multiply example can be shortened even further. So short, it's hard to remember there is seperate memeory allocation going on and a brand new execution context.

```js
const result = copyArrayAndManipulate([1,2,3], input => input*2);
```

## Pair Programming

The most effective way to grow as a software engineer. People can fall into some of the following habits / personas:

_Researcher_ avoids blocks by reading everything they can find on their block/bug

_Stackoverflower_ Uses code snippets to fix bug without knowing how they work

It's not that these personas are bad, but you need to balance them. It's ok to be reading and looking at others code, but don't do it too long. Seek to understand the code. Don't put off dealing with the block.

Pair programming:

* Tackle blocks with a partner
* Stay focused on the problem
* Refine technical communication
* Collaborate to solve problem
