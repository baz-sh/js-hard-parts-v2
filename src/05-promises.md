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

When the promise is complete and the data has been resolved and assigned within the promise object, then you can access it via the `then` method.

In the example, the display function is passed into the array of futureData's onFulfilled property to be run when completed.

![then](/img/05-then.png)

![then-2](/img/05-then-2.png)

Once the data comes back from twitter, the value is placed in `futureData`'s value property. This in turn triggers the onFulfilled array of functions to run. In this case `display`.

![then-complete](/img/05-then-complete.png)

**_then_ method and functionality to call on completion...**

Any code we want to run on the returned data must also be saved on the promise object.

Added using `.then` method to the hidden property `onFulfilment`.

Promise objects will automatically trigger the attached function to run (with its input being the returned data).

## Web APIs & Promises Example: fetch

Here is a breakdown and overview of how `fetch` works behind the scenes.

![fetch-example](/img/05-fetch-example.png)

## Web APIs & Promises Example: then

The promise object is designed by JS to automatically trigger the functions in the array of `onCompleted` to run with the value of the promise as the input when the value gets updated (e.g. when resolved the tweets from a twitter api call).

When you add a function with `then` this function gets added to the `onCompletion` array. When the value gets updated (e.g. when a network call resolves) the then function is called with the value field passed as the argument.

![then-example](/img/05-then-example.png)

## Web APIs & Promises Example: Microtask Queue




## Promises Review