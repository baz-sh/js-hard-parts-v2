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

So if I'm storing each user in my app with their respective data (let's simplofy)

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

## Factory Functions

## Factory Functions Example

## Prototype Chain

## Prototype Chain Example: Prototypal Link

## Prototype Chain Example: Implicit Parameters

## hasOwnProperty Method

## this Keyword

## Arrow Function Scoppe & this

## Prototype Chain Review

## new Keyword

## new Keyword Example

## class Keyword
