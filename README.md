[![Backbone.Giraffe](https://raw.github.com/barc/backbone.giraffe/master/src/docs/img/logo.png)](http://ryanatkn.github.io/backbone.giraffe)

# Backbone.Giraffe

### **!! ⮩** This is an archived fork of a project I was the main author of early in my career,
### the original repo is [@barc/backbone.giraffe/](https://github.com/barc/backbone.giraffe/),
### 🕸️ rip 🦒 2013—2015 🦴️

<hr />

## Introduction

[__Backbone.Giraffe__](http://ryanatkn.github.io/backbone.giraffe)
is a light and flexible library that extends
[__Backbone.js__](https://backbonejs.org/) to new heights.
__Giraffe__'s goal is to follow the __Backbone__ philosophy
to provide commonly needed features with few assumptions. It differs
from other Backbone libraries like __Marionette__ and __Chaplin__ in its
reduced scope and size, and it takes a different approach to the problems of
route handling, object lifecycles, event aggregation, and view management.

## Overview

- __Giraffe.View__ is a nestable and flexible class that provides lifecycle
management and many other useful features. It defaults to __Underscore__
templates and easily supports any form of templating.

- __Giraffe.App__ is a special view that helps your views, models, collections,
and routers communicate by acting as an event hub. Multiple apps can coexist and
teardown is as simple as it gets.

- __Giraffe.Router__ leverages an app's events to trigger routing events that
any object can listen for. It also has reverse routes to allow the construction
of URLs using app events and arguments.

- __Giraffe.Model__ and __Giraffe.Collection__ are thin wrappers that add
Giraffe's lifecycle management and app events. Any object can mix
in this functionality via `Giraffe.configure`.

## Documentation

Read the [__API docs__](http://ryanatkn.github.io/backbone.giraffe/backbone.giraffe.html) and
check out our [__live examples__](http://ryanatkn.github.io/backbone.giraffe/viewBasics.html).

## How Giraffe is Different

Giraffe was created by the needs of our team as we built
[__Barc__](http://barc.com). We tried many existing libraries but some did way too
much, others added too many layers, and others performed poorly.

Giraffe does not have all the bells and whistles of the larger frameworks.
We found the effort to customize them for our needs was more effort than simply
building upon Backbone with a minimalist approach. For example, there is no
concept of specialized containers like regions or layouts, as any view in
Giraffe can act as a parent of one or more child views. Giraffe also
has no CollectionView or ItemView
(see [__Giraffe.Contrib.CollectionView__](http://ryanatkn.github.io/backbone.giraffe/collectionView.html)
and [__Giraffe.Contrib.FastCollectionView__](http://ryanatkn.github.io/backbone.giraffe/fastCollectionView.html)),
but we are open to suggestions to make Giraffe as useful as possible to
Backbone developers who want an extension library with few opinions.

Is this framework for you? It depends. We feel Giraffe adds essential
features to make you more productive with Backbone.

### Highlights

- [__Routes emit events__](http://ryanatkn.github.io/backbone.giraffe/routersAndAppEvents.html)
instead of being tied to functions. This makes it extremely simple for a deeply
nested view to act on a route.

- [__Reverse routes with arguments__](http://ryanatkn.github.io/backbone.giraffe/backbone.giraffe.html#Router)
provide a way to trigger routes in the application using app events without
having to know a URL path.

- [__Giraffe.App__](http://ryanatkn.github.io/backbone.giraffe/appEvents.html) is a
special view that acts as an event hub to help your app communicate and respond
to routes, and all Giraffe objects have convenient `appEvents` bindings
inspired by `Backbone.View#events`.

- [__`Giraffe.View#attachTo(someElement)`__](http://ryanatkn.github.io/backbone.giraffe/backbone.giraffe.html#View-attachTo)
allows views to move anywhere on the DOM without clobbering each other's events,
and it automatically sets up parent-child relationships for memory management.

- [__Lifecycle management__](http://ryanatkn.github.io/backbone.giraffe/lifecycleManagement.html)
mitigates memory leaks. It's automatic for nested views and can be used for any
object with a `dispose` method via `Giraffe.View#addChild`.

- [__(A)sync app initialization__](http://ryanatkn.github.io/backbone.giraffe/appInitialization.html)
helps an app reach its ready state. For example, an app may need to wait for
asynchronous bootstrap data or a websocket connection before starting.

- [__Declarative event handling__](http://ryanatkn.github.io/backbone.giraffe/documentEvents.html)
in markup provides simple one-way binding. (does not try to be __Knockout__ or
__AngularJS__)

- [__Optional Giraffe.Contrib__](https://github.com/barc/backbone.giraffe/blob/master/src/backbone.giraffe.contrib.coffee)
extensions include a simple Controller class with Giraffe's lifecycle and `appEvents` features,
a [CollectionView](http://ryanatkn.github.io/backbone.giraffe/collectionView.html)
that renders a collection with a view per model,
and a [FastCollectionView](http://ryanatkn.github.io/backbone.giraffe/fastCollectionView.html)
that renders a collection with a single view
[more efficiently than Giraffe.Contrib.CollectionView and Marionette.CollectionView](http://jsperf.com/collection-views-in-giraffe-and-marionette/5).

## Download

__Version 0.2.8__

[backbone.giraffe.js](https://raw.github.com/barc/backbone.giraffe/master/dist/backbone.giraffe.js) _70.5k_

[backbone.giraffe.min.js](https://raw.github.com/barc/backbone.giraffe/master/dist/backbone.giraffe.min.js) _18.4k_

[backbone.giraffe.contrib.js](https://raw.github.com/barc/backbone.giraffe/master/dist/backbone.giraffe.contrib.js) _18.3k_

[backbone.giraffe.contrib.min.js](https://raw.github.com/barc/backbone.giraffe/master/dist/backbone.giraffe.contrib.min.js) _6.2k_

## Building

    npm install projmate-cli@0.1.0-dev -g
    npm install -d
    pm run all
    pm run all -ws # watches for file changes and runs local server at local.projmate.com:1080/dist/

## Changelog

### 0.2.8

- Fixed AMD loader.
- Added `Giraffe.noConflict` and `Giraffe.Contrib.noConflict`.
- `Contrib` now attaches itself as `root.GiraffeContrib` in addition to the existing `Giraffe.Contrib`.

### 0.2.7

- Fixed module loader for r.js optimizer.

### 0.2.6

- Configured objects (including all Giraffe objects) now have the following
  no-op function hooks for you to implement:
  `beforeDispose`, `afterDispose`, `beforeInitialize`, and `afterInitialize`.

- Disposed objects have a new property `_dispose` set to `true`.

### 0.2.5

- Support optional params for Router#isCaused and Router#cause. Optional static routes remain unsupported. See [issue 19](https://github.com/barc/backbone.giraffe/issues/19) for more.
- Contrib can now be required from the root: `require('backbone.giraffe/contrib')`.
- All invariants now throw errors instead of logging.

### 0.2.4

- Allow passing routing options to Giraffe.Router#cause.

### 0.2.3

- Fixed support for 0 as a path param.

### 0.2.2

- Added Backbone and Underscore CommonJS requires to Giraffe.Contrib.

### 0.2.1

- Fixed AMD loader check.

### 0.2.0

- Added support for AMD and node-style loaders.

- Put contributors in one place, the AUTHORS file.

- Using accurate semantic versioning, starting...now.

### 0.1.5

- Added events around several view methods: `rendering`, `rendered`,
  `attaching`, `attached`, `detaching`, `detached`

- ___BREAKING CHANGE:___ `dispose` now acts on `this` instead of taking the
  target object as an argument. Removed `disposeThis` as it's now redundant.

- Registered as a Bower package: `bower install backbone.giraffe`

### 0.1.4

- Added the function `Giraffe.configure` which 
  [mixes several Giraffe features](http://ryanatkn.github.io/backbone.giraffe/backbone.giraffe.html#configure)
  into any object. Used in the constructors of all Giraffe objects.

- `omittedOptions` can be used to prevent `Giraffe.configure` from extending
  particular properties. If the value is `true`, all properties are omitted.

- The document event prefix `'data-gf-'` is now configurable via
  `Giraffe.View.setDocumentEventPrefix` and as a parameter to 
  `Giraffe.View.setDocumentEvents` and `Giraffe.View.removeDocumentEvents`.

- ___BREAKING CHANGE:___ `dispose` is now mixed into configured objects
  with a default function, and is only copied if it doesn't exist.
  As a result, calls to super in `dispose` no longer make sense.
  Use `Giraffe.dispose` instead.

- `beforeDispose`, `afterDispose`, `beforeInitialize`, and `afterInitialize`
  are called if defined on all configured objects. Some are used by Giraffe
  objects so override with care.

- Added `Giraffe.wrapFn` which calls 'beforeFnName' and 'afterFnName' versions
  of a function name on an object. Here's a reference for future development - 
  [__Backbone.Advice__](https://github.com/rhysbrettbowen/Backbone.Advice)

## Contributors

View Giraffe's contributors [here](https://github.com/barc/backbone.giraffe/graphs/contributors)
or see the file [AUTHORS](https://github.com/barc/backbone.giraffe/blob/master/AUTHORS).

Suggestions and pull requests are welcome!

## License

Copyright (c) 2013 Barc Inc.

See the file [LICENSE](https://github.com/barc/backbone.giraffe/blob/master/LICENSE) for copying permission.

<p align="center">
  <a href="https://ryanatkn.github.io/backbone.giraffe">
    <img src="/dist/docs/img/backbone.giraffe.png" width="129" height="136">
  </a>
</p>
