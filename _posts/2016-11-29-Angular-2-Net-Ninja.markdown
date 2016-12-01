---
layout: post
title:  "Angular 2 - The Net Ninja Youtube Playlist"
date:   2016-11-29 07:00:17 -0600
categories: Angular2 SPA
---

#### The following are my notes from when I watched The Net Ninja's Angular 2 Playlist on Youtube.

[[Repository of final code](https://github.com/P1xt/ng2-demo-netninja)]

[[Live demo](http://p1xt-ng2ninja.surge.sh/)]

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

* dist folder - this is what gets deployed (auto-generated)
* e2e folder - ts config and end to end tests
* node_modules folder - auto-generated
* src folder - this is where all our awesome code goes
* various .json files - setup/config
* *.conf.js - for configuring testing

### Gotchas

**Note:** to make a css file that will affect the entire site, put it
in the src folder right next to the main index.html. The Ninja says to
put it in the public folder but angular-cli doesn't have that folder
any more. The src folder works.

**Note:** - The Ninja has us create a directives property on the
 Component Annotation object, this has been deprecated, now you set
 this up in the module.ts file using "declarations" instead of
 "directives". [example from TOH](https://angular.io/docs/ts/latest/tutorial/toh-pt3.html)

**Note:** - When the Ninja tells you to use the map function to map the
 data you get from `this.http.get()` to json you must ALSO add this to
 your includes `import 'rxjs/Rx';` or your console will fill up with
 errors, because without rxjs, the data you get from a http.get can't be
 manipulated with map.

**Note:** - When the Ninja tells you to use `HTTP_PROVIDERS` use
`HttpModule` instead, it changed between the filming of the videos
and the final release.


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
* **`ng generate pipe <name>`**- creates a new pipe with the name `<name>`
* **`ng generate service <name>`**- creates a new service with the name `<name>`


### Terminology

* **Component** - modular unit of the interface, composed of typescript,
html, css, and tests and may (optionally) contain other component.
* **Decorator** - (called Annotation in official Angular 2 docs)
Decorates a class (starts with @ and gives more information about a class).
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
    * property binding (`<input [required]='expression'>`) can bind to
    native html properties, built in angular directives, or
    custom made properties.
    * event binding (`<button(click)='expression/function'>`)
    * two way data binding (`<input [(ngModel)]="model/object">`)
* **routing** - mechanism by which angular knows which component to load
based on which url is browsed to (/home, /, /user, etc). Implemented by 
creating a routes file and exporting routes so they can be loaded in 
main.ts. Tells angular which component to load for each route and where
to load them. **Important note** The ng2 router has changed a lot since
the Ninja made his playlist. ROUTER_DIRECTIVIES wouldn't import so I
used RouterOutlet instead.
* **[ngClass]** - (attribute directive) - binds to an object like
 `<p [ngClass]="{'blue': true, 'red': false, 'underline': true}">`
 The object may be created in the component and used like
 `[ngClass]="classes"` where classes was created in the component
 constructor.
* **[ngStyle]** - (attribute directive) - Syntax:
`<span [ngStyle]="{background: ninja.belt}">{{ninja.belt}} belt</span>`
* **\*ngIf** - (structural directive) - only show element when the
 condition holds true. Syntax: `<p *ngIf="">only shown if true</p>`
* **\*ngFor** - (structural directive) - loop through list outputting
 html for each. Syntax: `<li *ngFor="let ninja of ninjas"></li>`
* **pipes** - reformat output - Syntax:
```<h3>{ { ninja.name | uppercase } }</h3>```
* **servie** - makes some functionality available throughout the app.
Example: databasse connection

### Firebase
Signup, grab the connect info, put it in index.html at the top level of
the app. Then you can do things like this to get and post data:

``` typescript
  fbGetData() {
    firebase.database().ref('/').on('child_added',
      (snapshot) => this.ninjas.push(snapshot.val())
    )
  }
  fbPostData(name, belt) {
    firebase.database().ref('/').push({name: name, belt: belt});
  }

```

list to display ninjas:

```
<ul id="ninja-listing">
  <li *ngFor="let ninja of ninjas | filter:term">
    <div class="single-ninja">
      <span [ngStyle]="{background: ninja.belt}">{{ninja.belt}} belt</span>
      <h3>{ {ninja.name} }</h3> // note the double { should be together
     </div>                     // for some reason it wouldn't print properly
  </li>
</ul>
```

form to add ninja:

```
<form id="add-ninja">
  <input type="text" [(ngModel)]="name" [ngModelOptions]="{standalone: true}" />
  <input type="text" [(ngModel)]="belt" [ngModelOptions]="{standalone: true}" />
  <button (click)="fbPostData(name, belt)">Add Ninja</button>
</form>
```
### Study materials


* [The Net Ninja Angular 2 Playlist](https://www.youtube.com/playlist?list=PL4cUxeGkcC9jqhk5RvBiEwHMKSUXPyng0) - currently watching
* [Assets Repository](https://github.com/iamshaunjp/angular-2-playlist)
