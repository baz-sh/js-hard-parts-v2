# Promises

## Promises Introduction

Promises are a two-pronged 'facade' funtions that both:

* Initiate background web broser work and
* Return a placeholder object (promise) immediately in JavaScript

```js
function display(data) {
    console.log(data);
}

const futureData = fetch('http://twitter.com/will/tweets/1');
futureData.then(display);

console.log("Me first!");
```

Fetch is a browser feature that is able to talk to the outside world. It also returns a little 'bonus' object that we are able to use in JS.

## Promises Example: fetch

![promises-example](/img/05-promises-fetch.png)

Fetch initiates the network request through the web browser, when the request is completed the value is placed within the "futureData" variables "value" property.

## Promises Example: then

## Web APIs & Promises Example: fetch

## Web APIs & Promises Example: then

## Web APIs & Promises Example: Microtask Queue

## Promises Review