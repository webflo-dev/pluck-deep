[![Build Status](https://travis-ci.org/landau/pluck-deep.svg)](https://travis-ci.org/landau/pluck-deep)

pluck-deep
==========

Pluck values of a collection given a 'dot' separated string

```js
module.exports = function pluckDeep(coll, selector) { ... }
```

## Install

`npm i -S pluck-deep`

## Usage

`deep-pluck` accepts an `array` or `object` as an initial argument.

You can pick a `value` or `array of values` by passing in a `selector`.

### Selectors

For the purpose of `deep-pluck` a `selector` is a `string` with object
value accessors separated with a `.`. In other words, you can retrieve
a value just like you would on any object, except that these selectors
will automatically `map` an array of values for you.

```js
// Example selectors
'planet.earth.size' // returns a single value set a size
'planet.saturn.moons.name' // Will return an array of moon names
```

> See below examples and tests for more selectors

### Value plucking

```js
var sel = 'mercury.venus';
var o = {
  mercury: {
    venus: 'earth'
  }
};

var v = pluckDeep(o, sel);
assert.equal(v, o.mercury.venus);
```

### Array plucking

```js
var sel = 'saturn.moons.name';
var o = {
  saturn: {
    moons: [
      { name: 'titan' },
      { name: 'enceladus' },
      { name: 'rhea' }
    ]
  }
};

var arr = pluckDeep(o, sel);
var expect = o.saturn.moons.map(prop('name'));
assert.deepEqual(arr, expect);
```

## Changelog

#### 0.1.1
- Added an extra santity test
