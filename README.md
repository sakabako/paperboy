Paperboy
===========

A simple event emitter and mixin.

[![browser support](http://ci.testling.com/sakabako/Paperboy.png)](http://ci.testling.com/sakabako/paperboy)

## Basic Usage

```javascript

var myObject = {'foo':'bar'};

var trigger = paperboy.mixin( myObject );

myObject.on('myEvent', function( howMany ) {
	console.log( howMany ); // 5
	console.log( this ); // myObject
});

trigger('myevent', 5);

```

## Methods

* `paperboy.emitter( /*[eventNames]*/ )`
 * Returns a new object with `on`, `one`, `off`, and `trigger` functions.
 * If an array of event names is passed it will be used as a whitelist of event names. An error will be thrown for anything different.
* `paperboy.mixin( target /*, [eventNames]*/ )`
 * Adds `on`, `one`, `off`, and `repeat` to `target`.
 * Returns the `trigger` function, _does not add it to the target_.

## Emitters

Emitters trigger event listeners. The `mixin` function turns any object into an emitter.

* `emitter.on( eventName, callback )` - adds a listener to the `eventName` event. `eventName` must be a string.
* `emitter.off( eventName, callback )` - removes a listener from an event.
* `emitter.one( eventName, callback )` - adds a listener that will remove itself after being triggered once.
* `emitter.repeat( otherEmitter /*, [eventNames] */ )` - Causes this emitter to repeat events triggered on another emitter.
* `emitter.trigger( eventName /*, additional, arguments */ )` - triggeres all event handlers for `eventName`.

NOTE: `trigger` is not added by the mixin function. If you want trigger to be public you must attach it to the target yourself.

## The Magic `*` Event

Listeners applied to the `*` event will be triggered for each event. The first argument will be the event name.

## Why Paperboy?

* Event listeners are always kept private.
* Passing in a whitelist of event names can prevent bugs.
* The `trigger` function is private by default, making it easier to write safe code. If you want it to be public simply add it to the target.
* Removing a listener in a callback will not cause it to skip the next listener.
* It's small, under 1k minified and gzipped.

Inspired by [LucidJS](https://github.com/RobertWHurst/LucidJS)
