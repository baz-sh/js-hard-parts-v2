# Asynchronous JavaScript

## Single Threaded Exection Review

Promises, async & the event loop

* Promises - the most significant ES6 feature
* Asynchronicity - the feature that mkes dynamic web applications possible
* The event loop - JavaScript's triage
* Microtask queue, Callback queue and Web Browser features (APIs)

JavaScript being single threaded means we can only do one thing at a time and the thread of execution moves down from one line to the other.

![synchronous](/img/04-synchronous.png)

## Asynchronicity in JavaScript

Asynchronicity is the backbone of modern web development in JavaScript yet...

JavaScript is:

* Single threaded (one command runs at a time)
* Synchronously executed (each line is run in order the code appears)

So what if we have a task:

* Accessing Twitter's server to get new tweets that takes a long time
* Code we want to run using those tweets

**Challenge:** We want to wait for the tweets to be stored in tweets so that they're there to run displayTweets on - but no code can run in the meantime.

JavaScript is not enough—We need a new pieces (some of which aren't JavaScript at all)

Our core JS enginer has 3 main parts:

* Thread of exectuion
* Memory/variable environment
* Call stack

We need to add some new components:

* Web Browser APIs/Node background APIs
* Promises
* Event loop, Callback/Task queue and micro task queue

## Asynchronous Browser Features

JavaScript often runs in the browser. The web browser has a whole bunch of extra functionaltiy beyond JS, to name a few:

* Dev tools
* Web sockets
* Network functionality
* Rendering engine
* HTML Dom

Although we don't find these features in JS, we can interface with them.

Some examples of  these interfaces are:

* setTimeout -> Timer
* document -> HTMLDom
* xhr/fetch -> Network Requests
* console -> console

There are other things like "local storage", "indexdb" etc. What's important is to realise that these things aren't features of JavaScript itself.

## Web API Example

```js
function printHello() { console.log("Hello");}

setTimeout(printHello, 1000);

console.log("Me first!");
```

This is processed / broken down as below:

![web-api-ex](/img/04-web-api.png)

## Web API Rules

As the browser has functionality we can lean on. e.g. creating a timeout, which is a browser / platform function, not JS, we are interacting with a world outside of JS. This means we need rules.

```js
function printHello(){console.log("Hello");}
function blockFor1Sec() {
    // blocks the JS thread for 1 sec, using a loop or something
}

setTimeout(printHello,0);
blockFor1Sec();
console.log("Me first!");
```

## Callback Queue & Event Loop

When we use things like `setTimeout` there is another queue in play. This is called the event loop. It is a queue of callbacks.

All code on the call stack has to be completed before anything from the event loop will be put on that stack. If the call stack is empty, it checks the queue and puts anything in there on the call stack. If not it just waits.
