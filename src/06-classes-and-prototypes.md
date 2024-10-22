# Classes & Prototypes

## Class & OOP Introduction

* An enormously popular paradigm for structuring our complex code
* Prototype chain - the feature behind-the-scenes that enables emulation of OOP but is a compelling tool in itself
* Understanding the difference between `__proto__` and `prototype`
* The `new` and `class` keywords as tools to automate our object & method creation

### Core of development (and running code)

1. Save data (e.g. in a quiz game the scores of user1 and user2)
2. Run code (functions) using that data (e.g. increase user 2's score)

Easy! So why is development hard?

In a quiz game I need to save lots of users, but also admins, quiz questions, quiz outcomes, league tables - all  have data and associated functionality

In 100,000 lines of code

* Where is the functionality when I need it?
* How do I make sure the functionality is only used on the right data!

### That is, I want my code to be

1. Easy to reason about

But also

2. Easy to add new features to (new functionality)
3. Nevertheless efficient and performant

The Object-oriented paradigm aims is to let us achieve these three goals.

## Object Dot Notation

So if I'm storing each user in my app with their respective data (let's simplify)

| User 1 | User 2 |
| ---- | ---- |
| name: 'Tim' | name: 'Stephanie' |
| score: 3 | score: 5 |

And the functionality I need to have for each user (again simplifying)

* increment functionality (in practice, there will be many functions)

How could I store my data and functionality together in one place?

### Objects store functions with their associated data

This is the principle of encapsualtion - and it's going to transform how we  can 'reason about' our code!

```js
const user1 = {
    name: "Sid",
    score: 3,
    increment: function() {user1.score ++}
};

user1.increment(); //user1.score -> 4
```

_Let's keeo creating our objects. What alternative techniques do we have for creating these objects?_

### Creating user2 using dot notation

Declare an empty object and add properties with dot notation

```js
const user2 = {};

//assign properties to that object
user2.name =  "Lem";
user2.score = 6;
user2.increment = function() {
    user2.score++;
};
```

## Factory Functions

`Object.create` is going to give us fine-grained control over our object later on

```js
const user3 = Object.create(null);

user3.name = "Eva";
user3.score = 9;
user3.increment = function() {
    user3.score++;
};
```

Our code is getting repetitive, we're breaking our DRY principle. And suppose we have millions of users! What could we we do?

## Factory Functions Example

```js
function userCreator(name, score) {
    const newUser = {};
    newUser.name = name;
    newUser.score = score;
    newUser.increment = function() {
        newUser.score++;
    };
    return newUser;
}

const user1 = userCreator("Sid", 3);
const user2 = userCreator("Lem", 5);
user1.increment();
```

This is what's known as a factory function. This is a function that returns an object.

## Prototype Chain

Rather than having each user object contain an increment function, ideally you want _one_ increment function that is the same but contained on each of the user objects.

![micro-task](/img/06-increment.png)

Solution: Using the prototype chain

Store the increment function in just one object and have the interpreter, if it doesn't find the function on user1, look up to that object to check if it's there.

Link user1 and fcuntionStore so the interpreter, on not finding `.increment` makes sure to check up in the functionStore where it would find it.

Make the link with `Object.create()` technique.

```js
function userCreator(name, score) {
    const newUser = Object.create(userFunctionStore);
    newUser.name = name;
    newUser.score = score;
    return newUser;
};

const userFunctionStore = {
    increment: function(){this.score++},
    login: function(){console.log("Logged in");}
};

const user1 = userCreator("Sid", 3);
const user2 = userCreator("Lem", 5);

user1.increment();
```

## Prototype Chain Example: Prototypal Link

![proto-link](/img/06-prototypal-link.png)

When JS doesn't find a given property (method or data) on an object it goes to the proto property and looks up the prototype chain to see if it can find that method or data.

## Prototype Chain Example: Implicit Parameters

When you use `Object.create()` it creates an empty object with a hidden `__proto__` property.

When you call `.increment()` on an object JS will look up the prototype chain to see if it can find the method. It does, and on the left of the .increment call `this` will be bound to the object the call has been invoked on. e.g. `user1.increment()`. This will access user1's score property that is used to increment.

## hasOwnProperty Method

What if we want to confirm our user1 has the property score?

```js
function userCreator(name, score) {
    const newUser = Object.create(userFunctionStore);
    newUser.name = name;
    newUser.score = score;
    return newUser;
}

const userFunctionStore = {
    increment: function() {this.score++},
    login: function() {console.log(`${this.name} logged in`)}
};

const user1 = userCreator("Sid", 3);
const user2 = userCreator("Lem", 5);
user1.hasOwnProperty('score');
```

When you run the `user1.hasOwnProperty('score')` what happens is JS looks for the method "hasOwnProperty" on the user1 object. It doesn't exist so it looks up the chain to userFunctionStore. This doesn't have it either so it follows it's proto chain until it hits `Object.prototype` which _does_ have the hasOwnProperty method. At which point it's grabbed and ran.

![proto-object](/img/06-proto-object.png)

## new Keyword

When we call the function that returns an object with `new` in front we automate 2 things.

1. Create a new user object
2. Return the new user object

But now we need to adjust how we write the body of userCreator - how can we:

* Refer to the uato-created object?
* Know where to put our single copies of functions?

## new Keyword Example

The new keyword automates a lot of our manual work.

```js
function userCreator(name ,score) {
    this.name = name;
    this.score = score;
}

userCreator.prototype.increment = function() { this.score ++ };
userCreator.prototype.login = function() { console.log("login"); };

const user1 = new userCreator("Eva", 9);

user1.increment();
```

![new-keyword](/img/06-new-keyword.png)

Introducing the keyword that automates the hard work: new

### Benefit

Faster to write. Often used in practice in professional code.

### Problems

95% of developers have no idea how it works and therefore fail interviews

We have to upper case first letter of the function so that we know it requires `new` to work.

## class Keyword

The class 'syntactic sugar'. We're writing our shared methods separately from our object 'constructor' itself (off in the `userCreator.prototype` object)

Other languages let us do this all in one place. ES2015 lets us do so too.

```js
class UserCreator {
    constructor(name, score) {
        this.name = name;
        this.score = score;
    }
    increment() { this.score++ };
    login() { console.log("login"); }
}

const user1 = new UserCreator("Eva", 9);
user1.increment();
```
