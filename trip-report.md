# Trip Report: MountainWest Hackweek 2014

I had the privilege of attending the [2014 MountainWest Hackweek](http://mtnwesthackweek.org/2014) in Salt Lake City, Utah, March 17-21.

Hackweek conducted in an auditorium @ the Salt Lake City Public Library, a beautiful and modern facility, and was composed of three separate conferences: a two-day JavaScript conference, a one-day DevOps conference and a two-day Ruby conference.

My notes from this conference are available @ https://github.com/erikj/mtnwest-2014-notes. Video of presentations should be available @ [Confreaks](http://www.confreaks.com/videos) within a few weeks of the conference.

## MountainWest JavaScript Conference

The JavaScript Conference covered the contemporary topics on JavaScript:

- latest-generation frameworks
- JavaScript build systems
- test-driven JavaScript and other best practices
- maintaining functionality for blind / vision-impaired users in an age of
increasingly graphically-based Web
- benchmarking JavaScript performance in Web applications
- ECMAScript 6's module functionality loading it into browsers that use ECMAScript 5

### Latest-Generation Frameworks

#### [React](http://facebook.github.io/react/index.html)

Pete Hunt, creator of what's considered the original JavaScript Model-View-Controller framework, [Backbone.js](http://documentcloud.github.io/backbone/), presented on the framework upon which he currently works Facebook's **React: A JavaScript Library For Building User Interfaces**.

**React** uses *"a virtual DOM diff implementation for ultra-high performance"*

A good way oo make user interfaces reliable is to use the technique of data binding. Many popular frameworks, *e.g.* Ember, Knockout, Backbone, etc. use key-value observation, but this consumes memory, which is limited on mobile devices. It is possible to monitor the Document-Object Model (DOM) of web pages, but the DOM is stateful (boo!).

However, `render` code is usually fast and cheap. So React leverages a Virtual DOM to keep track of only what's rendered, for *"ultra-high performance"*.

React is intended for complicated data views where the views are smaller than the model data which they represent. If models are smaller than the views, then *"your app is already fast"*

#### [RxJS: The Reactive Extensions for JavaScript](https://github.com/Reactive-Extensions/RxJS)

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

#### [Twitter Flight](http://twitter.github.io/flight/)

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

#### [Ember.js](http://emberjs.com/)

Many presenters mentioned that the framework they are using most is **Ember.js**. One presenter said during her introduction that it was her goal to not (otherwise) mention Ember during her talk. So it seemed clear that Ember is the dominant and preferred framework among this conference's presenters.

## MountainWest DevOps Conference

## MountainWest RubyConf

## Misc Observations

It appeared that there were as many presentations using [Reveal.js](https://github.com/hakimel/reveal.js) as Keynote, and they looked great. This is notable and promising for those of us who prefer to use familiar Web technologies over WYSIWYG presentation editors and opaque proprietary or binary formats.