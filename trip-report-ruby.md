# Trip Report: MountainWest RubyConf, March 20 & 21, 2014, Salt Lake City, Utah

The fourth and fifth days of MountainWest Hackweek were the [MountainWest RubyConf](http://mtnwestrubyconf.org/2014/), which is the original MountainWest technical conference, now in its @ least seventh year.

## Generate Parsers! Prevent Exploits!

Nick Howard, of Boulder's [Gnip](http://gnip.com/), presented a novel analysis and method for securely validating input in Ruby w/ the hypothesis:

> theory of computation is relevant to web development! (maybe)

Exploits arising from parsing of input are major security issues in web-application development. Nick asked:

> What do exploits have in common? They are unexpected computation. Exploits aren't tricks-- they're computational machines:
1. take input
2. do stuff
3. profit

> The same as usual programs.

Exploits pass input to make use of undocumented behavior. To prevent exploits, we must properly validate inputs, which can leverage the following theories of computation: [decidability](http://en.wikipedia.org/wiki/Decidability_(logic)), for certain types of input, decidability is proven impossible, and [Chomsky Hierarchy](http://en.wikipedia.org/wiki/Chomsky_hierarchy).

Additionally, we should recognize inputs before parsing them and can apply the concepts of [LANGSEC: Language-theoretic Security](http://langsec.org).

Nick then introduced his gem to address this problem: [muskox](https://github.com/baroquebobcat/muskox), a schema-based JSON parser generator that only allows valid strings to be parsed.

