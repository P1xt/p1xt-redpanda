---
layout: post
title:  "Angular 2 - The Net Ninja Youtube Playlist"
date:   2016-11-29 07:00:17 -0600
categories: Angular2 SPA
---

#### The following are my notes from when I watched The Net Ninja's Angular 2 Playlist on Youtube.

Component based! Navbar is a component, Sidebar too, everything. The 
application starts with a root component, which contains other
components, which in turn contain other components. So, for instance, 
the root component could contain sidebar, navigation, blog and footer 
components, each of which may, themselves, contain other components.

![Component Structure]({{ site.url }}/assets/component-graphic.png)


Each component is a modular unit of the overall application. It has it's own
html(view), css(styles), typescript(logic) and test(spec) files. It can
be imported into other components and then it's selector may be included
in that component's html in order to render it. You may include additional
 content within the selector and then have that additional content
 rendered wherever you like by using the `<ng-content>` directive to
 indicate where the content should be rendered within the component's
 html.

The tutorial is in TypeScript. The demo app created is Angular 2 (TypeScript)
with a Firebase backend.

#### Editor in use is Atom with the following plugins:

* platformio-ide-terminal
* language-typescript-grammars-only
* I also installed wakatime

### Setup

* first install node (I already had it installed, I'm running version 
7.2.0)
* `npm install -g angular-cli`
* Note: the Ninja said to setup the project wit `ng new projectname` but
I'd already created a git repo for it so I just cd'd into that and ran
`ng init`. Once that was finished, from the same directory I ran
`npm install` then, when that was finished, I ran `ng serve` and LO AND
BEHOLD when I browsed to `http://localhost:4200/` there was the cruddy
little do nothing starter Angular app!!!
* `ng build` builds the dist folder for deployment to production

### What did angular-cli create for us?

**Important note** - angular-cli has changed since the Ninja
made the videos, now you just get assets, e2e, node_modules, and src 
folders. And, you don't even get the dist folder until you do a
build. so **don't panic** angular-cli just cleaned up a bunch of
the boilerplate so there's less of it for you to worry about

**Note:** to make a css file that will affect the entire site, put it
in the src folder right next to the main index.html. The Ninja says to
put it in the public folder but angular-cli doesn't have that folder
any more. The src folder works.

* dist folder - this is what gets deployed (auto-generated)
* e2e folder - ts config and end to end tests
* node_modules folder - auto-generated
* src folder - this is where all our awesome code goes
* various .json files - setup/config
* *.conf.js - for configuring testing

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
    wheels: number = 4;
    speed: number; // note the type declaration

    constructor(mph:number) { // note constructor uses command line args
        this.sped = mph;
    }
    drive {
        console.log('the car is driving')
    }
}
myCar:Car = new Car(70)
```

#### Basic example of a component

``` typescript
import { Component } from '@angular/core';

@Component({ // component decorator decorates the class that follows
    moduleId: module.id,  // use moduleId if you want relative urls
    selector: 'app-root', // html tag where this component is bound
    templateUrl: 'app.component.html', // relative url
    styleUrls: ['app.component.css']   // relative url
})
export class AppComponent { // decorated by @Component
    title = 'app works!';   // proporties this comoponent can use
}
```

#### ng commands

* **`ng generate component <name>`** - creates a new component with the name
`<name>`. Note, run this command from within the src/app directory to
ensure that the new component is created within app.

### Terminology

* **Component** - modular unit of the interface, composed of typescript,
html, css, and tests and may (optionally) contain other component.
* **Decorator** - Decorates a class (starts with @ and gives more information
about a class).
* **Import** - used to pull in resources from another file.
* **Template** - html file containing the structure of a component, included
via the **templateUrl** property of the object passed in the Component
decorator OR html directly included in the **template** property of the
object passed in the Component decorator.
* **OnInit** - imported from Angular/Core to make available processing
when a component is initialized.
* **Nested Component** - Component that should be rendered inside another
component. You MUST import it in the component you want to nest it
inside. You must also add it to the "directives" property of the main
component's decorator object. (note, the Ninja says to import index, but
the new cli will create for instance home.component.ts if you create
a component named home so you should use home.component, not index).
* **ng-content directive** - allows you to include some content inside
a nested component that is entered into the main component. Include the
content inside the nested component's tags in the main component's html,
and then use the `<ng-content>` tag within the html for the nested
component to pinpoint where that content should be placed.
* **data binding** - use
    * string interpolation (double curly braces)
    * property binding (`<input [required]='expression'>`)
    * event binding (`<button(click)='expression/function'>`)
    * two way data binding (`<input [(ngModel)]="model/object">`)

### Study materials

* [The Net Ninja Angular 2 Playlist](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jqhk5RvBiEwHMKSUXPyng0) - currently watching
* [Assets Repository](https://github.com/iamshaunjp/angular-2-playlist)
