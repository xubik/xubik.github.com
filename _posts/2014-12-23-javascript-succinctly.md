---
layout: post
title: Javascript Succinctly
---
{% include JB/setup %}

## Preface

Mozilla javascript reference: <https://developer.mozilla.org/en-US/docs/Web/JavaScript>
David Flanagan: TODO look up

## Chapter 1: JavaScript Objects

### Creating objects

An object in JavaScript is just a container for properties, each of which has a name and a value.
Methods are just properties which contain a `Function()` object.

New objects can be created by calling the `new Object()` constructor function. 
User defined contructor functions can also be defined to create custom objects:
```
var Person = function (living, age, gender) {
        this.living = living;
        this.age = age;
        this.gender = gender;
this.getGender = function () { return this.gender; }; };
```

Conventionally, a capital letter is used (i.e. `var Person`, not `var person`).

Objects created from either `new Person()` or `new Object()` with the same properties will be exactly the same object. Only the method of creating is different.

### JavaScript constructors create and return object instances

A constructor function is a cookie cutter for producing objects that have default properties and property methods.
The *only difference* between a constructor function and a normal function is how it behaves when invoked with the `new` keyword. In this case, JavaScript sets the value of `this` to the new object being created and returns it (instead of false).

### The native JavaScript object constructors

`Number(), String(), Boolean(), Object(), Array(), Function(), Date(), RegExp(), Error()`

JavaScript is mostly constructed from these nine native (aka global) objects as well as the string, number and Boolean primitive values. 

Note, `Math` is a static object, a container for methods (and therefore not instantiated using the `new` keyword).

### Instantiating constructors using the new operator

Constructor functions can be called with or without the `new` keyword.

If called without using `new`:
* the `this` referred to in a constructor function is no longer the object under construction, but the parent object (see Chapter 6)
* the object is not returned (the constructor function could always explicity return the object)

You can log `myobj.constructor` to see the function definition (which for the built in types won't show you the actual defnition, but for an unknown type, will at least reveal how it was created and therefore reveal its type).

### Creating shorthand or literal values from constructors

_Literals_ are shorthand for creating objects for the built in types rather than calling the `new` keyword.

* Number - just use the number
* String - use quotes
* Boolean - true or false
* Object - {}
* Array - []
* Function - function(x, y) { return x* y };
* RegExp - //

In general the effect is exactly the same as using the `new` keyword. However, in the case of number, string and boolean types, a complex object is not created until object properties are used. e.g `'foo'.length`. Only at this point does a _wrapper_ object get created and then discarded again afterwards.

### Primitive (aka simple) values

The JavaScript values `5`, `'foo'`, `true`, and `false` , as well as `null` and `undefined`, are considered primitive because they are irreducible. 

Note, if using the `new` keyword to create String, Number or Boolean types, then complex objects *are* created and returned. 

Note, if you alternatively call the String(), Number() or Boolean() constructor functions without the `new` keyword, the primitive values are returned. *In this instance, are the complex objects constructed or not - I assume not.*

Primitive values are stored and copied by value, and are equal if equal in value.

### Complex objects (aka composite objects or reference types)

Complex values are stored and manipulated by reference. They are equal only if referring to the same reference (address).

### The typeof operator used on primitive and complex values


