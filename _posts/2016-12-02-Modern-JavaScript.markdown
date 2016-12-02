---
layout: post
title:  "Modern JavaScript"
date:   2016-12-02 06:00:17 -0600
categories: Angular2 SPA JavaScript
---

## Overall Impression

The first part of this tutorial was decent, then, the production quality
went downhill fast. Volume varied widely between video to video, so some
I had to turn my volume all the way up, then the next video would be
crazy loud.

Overall, this is good as a blueprint of what to lookup SOMEWHERE ELSE
to ensure you're up to speed with the current state of JavaScript.
Especially in the TypeScript section, I found myself just hitting the
official TypeScript docs when I got to each section and reviewing the
concepts there.

Underscore and RxJS were both just tossed into the middle of lessons
with little to no fanfare, making it unclear that they were external
libraries, and with no instructions for any sort of best practice for
including them.


## My Notes

These are my notes from a quick pre-course for angularclass.com's Angular 2 Fundamentals
course. It covers some ES5, ES6, and TypeScript to lay a baseline foundation
in JavaScript/TypeScript for the Angular 2 Course.

### ES6

#### Var, Let & Const

* var - is hoisted
* let - is the same as var but is scoped to whatever curly braces it's
defined inside, it is not hoisted.
* const - is just like let but the value cannot be changed after it is
initially assigned

#### Arrow Functions

* maintain parent object scope inside a callback
* are anonymous (you can't give them a name) functions
* Syntax: `(a) => a + 1` replaces `function(a) { return a + 1; }`

#### Template Strings

* let you put multiline strings inside backtics
* let you use string interpolation inside the string `${ somevariable }`

#### Destructuring

* lets you dynamically extract properties off a data structure and
assign them to separate variables
* Syntax: `let {a, b} = object;` where object contains properties for a and b.

#### Rest Parameters

* if the last argument is prefixed with ... it will contain all the "rest"
of what was passed in.
* Syntax: `(...args) => console.log(args)` - args will contain ALL arguments
to the function.
* useful for when there are a varying number of arguments coming into a
function. If you use the rest operator, you can gather them all into an
array you can iterate over.

#### Spread Operator

* Looks just like the Rest Parameter, but it's actually the opposite
* It takes an object and expands it out to distinct values.
* `...[1, 2, 3]` becomes `1, 2, 3` - separate values that can be passed
to a function, etc

#### Enhanced Object Literals

* shorthand syntax for initializing properties from variables and
defining object methods
* `var1, ` - is the same as `var1: var1`
* can use computed values now such as `['text' + var]: value, `
* can now omit function keyword and colon when declaring methods in objects.

#### Classes

Syntax:

``` javascript
class App { // convention - class name PascalCase
    contructor() {
        // some stuff to do when we spin the class up
    }

    some_function() {
        // some method the class makes available
    }
}

var app = new App();
app.some_function();
```

#### Modules

* allow code sharing between javascript files
* export from one file `export var x = 'some value';`
* import from another file `import { something } from 'somewhere';`

### TypeScript

* superset of JavaScript

#### Types

* lets us explicitly define types like - `var age: number = 12`
* string, number, boolean - basic types
* catches it if we try to put data of one type into a variable expecting
a different type.
* can use types in function declarations as well to ensure the function
only accepts data of the appropriate type

#### Interfaces

* blueprint for an object
* explicitly details what methods and variables are required to define
 an object of a particular type.
* can contain optional properties

Syntax (from [The offical TypeScript Docs](https://www.typescriptlang.org/docs/handbook/interfaces.html))




``` typescript
interface SquareConfig {
    color?: string;
    width?: number;
}

function createSquare(config: SquareConfig): {color: string; area: number} {
    let newSquare = {color: "white", area: 100};
    if (config.color) {
        newSquare.color = config.color;
    }
    if (config.width) {
        newSquare.area = config.width * config.width;
    }
    return newSquare;
}

let mySquare = createSquare({color: "black"});

```

#### Classes

Syntax (from [The offical TypeScript Docs](https://www.typescriptlang.org/docs/handbook/classes.html))

Note - look at the docs, there's a lot more info about public, private,
and static variables, inheritance, etc.



``` typescript
class Animal {
    name: string;
    constructor(theName: string) { this.name = theName; }
    move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Snake extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 5) {
        console.log("Slithering...");
        super.move(distanceInMeters);
    }
}

class Horse extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 45) {
        console.log("Galloping...");
        super.move(distanceInMeters);
    }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);
```

#### Decorators

(from [The offical TypeScript Docs](https://www.typescriptlang.org/docs/handbook/decorators.html))

A Decorator is a special kind of declaration that can be attached to a class declaration, method, accessor, property, or parameter. Decorators use the form @expression, where expression must evaluate to a function that will be called at runtime with information about the decorated declaration.

### Node.js

* bunch of nonsense about using underscore that I made wanking motions and didn't listen to much

#### NPM

* npm - node package manager, used to define and download/install
dependencies
* npm install to download our dependencies locally
* node_modules/ folder for our dependencies
* package.json and npm init - init creates project and sets up package.json,
which in turn contains configuration settings for scripts and dependencies
* npm scripts - allow you to run tests, start the application, do build
tasks, stc
* dependencies and devDependencies - separate out what you need while
developing as compared to what you'd deploy as part of a production build
* npm install --global for CLI
* npm uninstall and npm uninstall --global - to uninstall

#### Promises

Promises allow us to pass around a chain of asynchronous tasks that will
be fired off as soon as the promise is created. We use Promises as a better
way to deal with writing async flow control compared to callback style.
Doing so allows us to reason about what is happening within our codebase
by isolating logic that starts off asynchronous operations.

Callback style is great only for one level compared to nested callbacks.
Trying to understand what is available to us within a callback can be
challenging with we’re more than one callback deep.

A promise object simply has a .then that we can invoke with our callback.
You can think of a promise like a gift wrapped present that is opened
once we reached a certain time or event. We can only open the present
once to get it’s value. The .then() callbacks are actions that we fire
off after the initial promise is resolved (in our analogy our present
is resolved once we reached a certain date).

The best feature of promises are the chains we can create. We create a
promise chain by simply invoking .then() and providing a callback.
We can also return another promise that needs to be resolved before
continuing down our promise chain

Catching errors is another great aspect of promises because it gives
us a standard way of interacting with errors. If we include a .catch
in the middle of our promise chain then any errors thrown before it
will be caught. We can now choose to rethrow to continue to the next
.catch call or handle the error and pass a value that will continue the chain.

We can also return other values rather than using throw by returning
a wrapped value with Promise.reject()

We can also fire off many async tasks and wait until they are all done
before running another task. Composing promises are great because
Promise.all() also returns another promise.

We can create our own promise to wrap other async interfaces or any
custom asynchronous tasks that we want to create a standard way of
interacting.

#### Then, with no warning RxJS

I stopped here as it seemed pretty slapdash, much like how the series
started with Underscore, without explaining what it was, or how to
include it in a project, this section jumped right into RxJS without
explaining that, unlike promises, this was an external library. And,
only one part of that library at that.

#### Webpack

Skipping the Webpack section, I'll hit the Net Ninja's playlist if
I need a review.

### Study materials

* [Modern JavaScript](http://courses.angularclass.com/courses/modern-javascript/)

