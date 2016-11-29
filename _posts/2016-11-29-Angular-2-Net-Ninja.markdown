---
layout: post
title:  "Angular 2 - The Net Ninja Youtube Playlist"
date:   2016-11-29 07:00:17 -0600
categories: Angular2 SPA
---

#### The following are my notes from when I watched The Net Ninja's Angular 2 Playlist on Youtube.

Component based! Navbar is a component, Sidebar too, everything :)
Tutorial is in TypeScript. Demo app created is Angular 2 (TypeScript)
with a Firebase backend.

#### Editor in use is Atom with the following plugins:

* platformio-ide-terminal
* language-typescript-grammars-only
* I also installed wakatime

### Setup

* first install node (I already had it installed, I'm running version 
7.20.0)
* `npm install -g angular-cli`
* Note: the Ninja said to setup the project wit `ng new projectname` but
I'd already created a git repo for it so I just cd'd into that and ran
`ng init`. Once that was finished, from the same directory I ran
`npm install` then, when that was finished, I ran `ng serve` and LO AND
BEHOLD when I browsed to `http://localhost:4200/` there was the cruddy
little do nothing starter Angular app!!!

### TypeScript quick start

Typescript is a superset of JavaScript, it has ALL of JavaScript, plus
some extra stuff like types, classes, and more.

#### Declaring variables in TypeScript.

* once you declare a variable and use it as a particular type (number, 
string, boolean, any) you can NOT then use it for a different type later.
* typically you explicitly state the type in the variable declaration,
for instance: `myVar:string = "hello"` or `myVar:number = 20`

#### Classes
``` typescript
class Car {
    wheels:number = 4

    drive {
        console.log('the car is driving')
    }
}
myCar:Car = new Car()
```

### Study materials

* [The Net Ninja Angular 2 Playlist](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jqhk5RvBiEwHMKSUXPyng0) - currently watching
* [Assets Repository](https://github.com/iamshaunjp/angular-2-playlist)
