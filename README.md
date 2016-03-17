# Bonus: Using the component() method

## Overview

Angular 1.5 brought the awesome `.component` directive. Don't worry, the learning curve isn't massive - it's basically a simplified directive!

## Objectives

- Describe component() and directive() differences

## component()

We use components every day - be it a dropdown box, a login form or a navigation bar. Components are awesome - much like directives, they're reusable, isolated pieces of functionality that we can use again and again. Other frameworks provide similar abilities - in fact the whole of React is based off of components - nothing else!

Instead of passing through a function to our `component` method (like what we do with the `directive` method), we pass through an object instead. This is really similar to the object we return in our directives.

For example:

```js
function Counter() {
	return {
		template: [
			'<div ng-click="counter.increment()" class="counter">',
				'<h3>Counter</h3>',
				'<div>Click anywhere to increment the counter!</div>',
				'<div class="counter__count">Current count: {{ counter.count }}</div>',
			'</div>'
		].join(''),
		controller: function ($scope) {
			this.count = 0;

			this.increment = function () {
				this.count++;
			};
		},
		controllerAs: 'counter'
	}
}

angular
	.module('app')
	.directive('counter', Counter);
```

Would turn into this:

```js
var Counter =  {
	template: [
	    '<div ng-click="counter.increment()" class="counter">',
	        '<h3>Counter</h3>',
	        '<div>Click anywhere to increment the counter!</div>',
	        '<div class="counter__count">Current count: {{ counter.count }}</div>',
	    '</div>'
	].join(''),
	controller: function ($scope) {
	    this.count = 0;

	    this.increment = function () {
	        this.count++;
	    };
	},
	controllerAs: 'counter'
};

angular
	.module('app')
	.component('counter', Counter);
```

Pretty much the same thing! However, there are a few restrictions to using the `.component()` method:

- Every item is an element - we can't create attributes
- We no longer use the `scope` property. Everything is bound to the controller
- We no longer use `bindToController` - this is simply named `bindings` instead
- When we use `require`, we have to pass through an object instead of a string, with the property being anything that we want and the string being what we'd normally use
    - For example, instead of `{ require: '^parentController' }`, we use `{ require: { parent: '^parentController' } }`
- We cannot use a `link` or `compile` function

Then why even use them? Well, directives are old and a bit verbose for what we may need 99% of the time. Components are a new, updated method that has matched the way the frontend has changed. Think of them as a simple way to write a directive, and if you need to go complicated, use a directive instead.