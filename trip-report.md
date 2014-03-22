# Trip Report Mountain-West Hackweek 2014

I had the privilege of attending the [2014 Mountain-West-Hackweek Conference](http://mtnwesthackweek.org/2014) in Salt Lake City, Utah, March 17-21.

The conference was conducted in an auditorium @ the Salt Lake City Public Library, a beautiful and modern facility, and was composed three separate conferences: a two-days JavaScript conference, a one-day DevOps conference and a two-day Ruby conference.

## JavaScript

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

#### [Ember.js](http://emberjs.com/)

Many presenters mentioned that the framework they are using most is **Ember.js**. One presenter said during her introduction that it was her goal to not (otherwise) mention Ember during her talk. So it seemed clear that Ember is the dominant and preferred framework among this conference's presenters.

## DevOps

## Ruby
