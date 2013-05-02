# Class  [![Build status][travis-image]][travis] [![Code coverage status][coveralls-image]][coveralls]
> A JavaScript OOP framework for Node.js and the browser

#### Sweet syntactic sugar for prototypal inheritance.
Class adds `construct()`, `destruct()`, `_super()`, and an `init()` method that runs after construction is complete.

#### Not afraid to mix it up.
Mixins can be added when a class is declared or after instantiation with the `mixin()` method.

#### Crushes boilerplate with a classy touch.
Stay classy and boilerplate-free with string-based `toString` declarations and automatic chaining of `construct()` and `destruct()`.


## Dependencies

Class is completely standalone with no dependencies. All you need to stay classy is [`Class.js`][Class.min.js].


## Compatibility

Class is compatible with the latest modern browsers and the oldest versions of Node.js and even IE 5 (with the use of [`Class.polyfills.js`][Class.polyfills.min.js]).


## Usage

Class empowers you without getting in your way. See the examples below to see how Class makes prototypal inheritance painless.


### Define a class

```javascript
var Parent = Class({
	toString: 'Parent',
	construct: function() {
		console.log('Parent: Constructing');
	},
	destruct: function() {
		console.log('Parent: Destructing');
	},
	doStuff: function() {
		console.log('Parent: Doing stuff');
	}
});
```


### Define a mixin

```javascript
var stuffDoer = {
	doStuff: function(_super) {
		_super.call(this);
		console.log('Mixin: Doing stuff');
	}
};
```


### Inherit from Parent and add a mixin to the class prototype

Mixins added at declaration time become part of the prototype.

```javascript
var Child = Parent.extend({
	toString: 'Child',
	mixins: [stuffDoer],
	construct: function() {
		console.log(this+': Constructing');
	},
	destruct: function() {
		console.log(this+': Destructing');
	},
	doStuff: function(_super) {
		_super.call(this);
		console.log(this+': Doing stuff');
	}
});
```


### Create an instance

```
var child = new Child(); // The new keyword is optional
/* Output:
	Parent: Constructing
	Child: Constructing
*/
```


### Call a method

```javascript
child.doStuff();
/* Output:
	Parent: Doing stuff
	Child: Doing stuff
	Mixin: Doing stuff
*/
```


### Add a mixin to the instance

Mixins added after instantiation become part of the instance.

```javascript
child.mixin({
	doMoreStuff: function() {
		console.log(this+': Doing more stuff')
	}
});

child.doMoreStuff();
/* Output:
	Child: Doing more stuff
*/
```


### Check yo' self

```javascript
console.log(child.instanceOf(Child)); // true
console.log(child.instanceOf(Parent)); // true
console.log(child.constructor === Child) // true
console.log(child+''); // 'Child'
```


### Wreck yo' self

```javascript
child.destruct();
/* Output:
	Child: Destructing
	Parent: Destructing
*/
```

## License

Class is licensed under the permissive BSD license.


[Class.min.js]: http://lazd.github.io/Class/build/Class.min.js
[Class.polyfills.min.js]: http://lazd.github.io/Class/build/Class.polyfills.min.js

[coveralls]: https://coveralls.io/r/masyl/Class
[coveralls-image]: https://coveralls.io/repos/masyl/Class/badge.png?branch=master

[travis]: http://travis-ci.org/lazd/Class
[travis-image]: https://secure.travis-ci.org/lazd/Class.png?branch=master
