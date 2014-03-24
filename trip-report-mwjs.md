# Trip Report, MountainWest JavaScript Conference, March 17 & 18, 2014, Salt Lake City, Utah

The JavaScript Conference covered the contemporary topics on JavaScript:

- latest-generation frameworks
- JavaScript build systems
- test-driven JavaScript and other best practices
- maintaining functionality for blind / vision-impaired users in an age of
increasingly graphically-based Web
- benchmarking JavaScript performance in Web applications
- ECMAScript 6's module functionality loading it into browsers that use ECMAScript 5

## Latest-Generation Frameworks

### [React](http://facebook.github.io/react/index.html)

Pete Hunt, creator of what's considered the original JavaScript Model-View-Controller framework, [Backbone.js](http://documentcloud.github.io/backbone/), presented on the framework upon which he currently works Facebook's **React: A JavaScript Library For Building User Interfaces**.

**React** uses *"a virtual DOM diff implementation for ultra-high performance"*

A good way oo make user interfaces reliable is to use the technique of data binding. Many popular frameworks, *e.g.* Ember, Knockout, Backbone, etc. use key-value observation, but this consumes memory, which is limited on mobile devices. It is possible to monitor the Document-Object Model (DOM) of web pages, but the DOM is stateful (boo!).

However, `render` code is usually fast and cheap. So React leverages a Virtual DOM to keep track of only what's rendered, for *"ultra-high performance"*.

React is intended for complicated data views where the views are smaller than the model data which they represent. If models are smaller than the views, then *"your app is already fast"*

### [RxJS: The Reactive Extensions for JavaScript](https://github.com/Reactive-Extensions/RxJS)

Two presentations on **RxJS** were delivered by Netflix employees. **RxJS** is a reactive JavaScript framework based on functional programming. When writing interface interactions in JavaScript, events and *callback hell* are known points of pain. Commenting on Netflix' use of **RxJS**, one presenter commented: *"Nowadays, I don't think in terms of events, I think in terms of collections"*.

In functional programming, collections are handled w/:

- `map`: transforms data
- `filter`: narrows colletions
- `reduce`: turns a collection into single value
- `zip`: combines two collections

Reactive programming offers these collection-flattening patterns:

- `merge`
- `[concat](https://github.com/Reactive-Extensions/RxJS/blob/master/doc/api/core/observable.md#rxobservableconcatargs)`
- `switchLatest`

The other Netflix presenter stated *"at Netflix, we only try to manipulate data within `forEach` loop"*. This is much easier to work w/ than writing code that has to wait for AJAX or other callbacks waiting to be asynchronously triggered by server responses.

### [Twitter Flight](http://twitter.github.io/flight/)

Another JavaScript framework that was a topic of a presentation was **Twitter Flight**. In ["You should be using Twitter's Flight framework."](http://kperch.github.io/mtn_west/) Kassandra Perch described the framework as:

- set of small utilities
- encourages well-written, modular apps
- lightweight
- not MV* (Model View Controller, Model View Whatever, etc.)
- plays well w/ other libraries, *e.g.* AngularJS, Ember, *et. al*
- gives you tools to structure your code

The commandments of **Flight** are:

- components are atomic
- communication vie events
- use the DOM
- test everything

**Flight** is big on functional mixins, per the Gang of Four [Design Patterns](http://en.wikipedia.org/wiki/Design_Patterns), we should value object Composition over Inheritance.

The steps to incorporate into your own code were described as:

1. write your html
2. write your JS component code
  - `this.defaultAttrs({})`
    - allows easy overrides without changing class
  - `this.after('initialize', function(){})`
  - Event handlers, listeners
3. run `.attachTo(selector)`

**Flight** provides utilities needed for testing an application's JavaScript:

- components = tiny little services
- each service has a consistent API
- JavaScript-test-framework extensions: [jasmine-flight](https://github.com/flightjs/jasmine-flight), [mocha-flight](https://github.com/flightjs/mocha-flight)
- wrappers:
  - set up `EventSpies`
  - automate HTML markup injection
  - headless test running

### [Ember.js](http://emberjs.com/)

Many presenters mentioned that the framework they are using most is **Ember.js**. One presenter said during her introduction that it was her goal to not (otherwise) mention Ember during her talk. So it seemed clear that Ember is the dominant and preferred framework among this conference's presenters.

#### Ember.js + TDD

Two presentations were given on doing Test-Driven Development w/ Ember.js: *Using TDD to Tame the Big Ball o' Mud* by Brandon Hays of [The Frontside](http://frontside.io/) and *Test-Driven Development of Ember.js Applications * by Andy Pliszka of Pivotal Labs. Both were based on usage of the [Jasmine BDD framework](http://jasmine.github.io/).

Andy's presentation was based on a  demo "TODO" JavaScript application that has code located at https://github.com/AntiTyping/EmberDo.

## And benchmarks for all!

Alex Navasardyan, a member of the Ember.js release-management team, delivered a presentation on benchmarking JavaScript, *e.g.* applications and libraries. For benchmarking JavaScript web applications, it can be difficult to obtain useful benchmarks by looping through execution of code, due to browsers' aggressive garbage collection and compiler optimizations. He recommended using a dedicated library, such as [benchmark.js](http://benchmarkjs.com/) or service, *e.g.* [jsPerf](http://jsperf.com/)

## Browser Package Management

Guy Bedford spoke on a point of frequent pain for JavaScript developers working on browser-side web applications and Node.js applications: package management. [Require.js](http://requirejs.org/) is a popular solution to this problem, encouraging modularity and making it easy to share code between applications, but configuration is a massive pain: very repetitive and not easily shared. The goal is for a developer to open a web browser and start developing, without the need to install a package manager.

Two possible solutions to this issue are:

- [jspm](http://jspm.io/), *"Frictionless browser package management"*

  > jspm loads any module format (ES6, AMD, CommonJS and globals) directly from endpoints such as `npm` and `github` over CDN for easy in-browser package management.

- [browserify](http://browserify.org/)

  > Browserify lets you require('modules') in the browser by bundling up all of your dependencies.

### jspm

**jspm** is based on [systemjs](https://github.com/systemjs/systemjs), a *"Spec-compliant universal module loader - loads ES6 modules, AMD, CommonJS and global scripts."* and [ES6 Module Loader Polyfill](https://github.com/ModuleLoader/es6-module-loader), which *"Dynamically loads ES6 modules in NodeJS and current browsers."* ES6 Module Loader Polyfill *"Uses [Traceur](https://github.com/google/traceur-compiler) for compiling ES6 modules and syntax into ES5 in the browser with source map support."*

#### jspm vs. browserify

Guy presented a benchmarks of jspm vs. browserify using the [voxel engine](https://github.com/maxogden/voxel-engine), demonstrating the browserify bundle has a much faster load time, but also a much slower compile time than jspm, which makes jspm the winner of this benchmark, as compile time is typically slower than load time.

## Lightning Talks

Among the notable lightning talks that were delivered @ MountainWest Javascript were:

**Nick Howard: Higher-Order Functions in 120 Seconds**, which are functions that input and return functions, *ie.* combinators. He introduced [`allong.es`](http://allong.es/), *"a JavaScript library based on the function combinator and decorator recipes introduced in the book JavaScript Allongé."*

An introduction to the [**Unicorn Law**](http://geekfeminism.wikia.com/wiki/Unicorn_Law), which states that *"If you are a woman in Open Source, you will eventually give a talk about being a woman in Open Source."*

**[Middleman](http://middlemanapp.com/): for javascript builds**. Middleman is a Ruby gem that, like the familiar Rails-asset pipeline, uses [Sprockets](https://github.com/sstephenson/sprockets). Middleman allows you to build static and optimized web sites using familiar dynamic tools, such as CoffeeScript, Sass, ERB, Haml, etc.
