iteration-typeguards
====================
[![NPM](https://nodei.co/npm/iteration-typeguards.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/iteration-typeguards/)

[![Build Status](https://jenkins.selenotrope.space:8443/buildStatus/icon?job=iteration-typeguards)](https://jenkins.selenotrope.space:8443/job/iteration-typeguards/)
[![npm version](https://badge.fury.io/js/iteration-typeguards.svg)](https://badge.fury.io/js/iteration-typeguards)

Installation
------------
Install with npm

    npm install iteration-typeguards

Requirements
------------
This module assumes a javascript environment implementing ES6, as it defines iterators and
iterability based on the [ES6 iteration protocols](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Iteration_protocols).

Usage with Typescript
---------------------
A typescript compiler `--target` argument of `es6` should be used. Both of the functions
isIterable and isIterator are defined as typescript typeguards for the built-in iterfaces:
Iterable<T> and Iterator<T>, respectively.

### isIterable

```typescript
import {isIterable} from "iteration-typeguards";

isIterable(5);                                                            // false
isIterable<string>("oh hai");                                             // true
isIterable(null);                                                         // false
isIterable([1,2,3]);                                                      // true
isIterable(new Map<any,any>([["hi", 3], [{water: true}, "summer"]]))      // true
isIterable({
  [Symbol.iterator]: function() {
              return {
                next: function() {
                  return 47;
                },
                done: false
              }
            }
});                                                                         // true
```

### isIterator

```typescript
import {isIterator} from "iteration-typeguards";

isIterator(5);                                                              // false
isIterator<string>("oh hai");                                               // false
isIterator<string>("oh hai"[Symbol.iterator]());                            // true
isIterator(null);                                                           // false
isIterator([1,2,3]);                                                        // false
isIterator([1,2,3][Symbol.iterator]);                                       // true
isIterator({
  next: function() {
    return 47;
  },
  done: false
});                                                                         // true
```

Usage without Typescript
------------------------
Usage without typescript in nodejs is very similar to the typescript examples above
without the type annotations. Since an ES6 environment is assumed, the import statements
above should work. The more traditional nodejs require statements shown below also work.

```javascript
var itGuards = require("iteration-typeguards");

itGuards.isIterable([1,2,3])                                                // true
itGuards.isIterator([1,2,3][Symbol.iterator])                               // true
```

Contribution
------------
If you come across a case in which these typeguards do not perform as expected, please
submit an issue (outlining the case) or a pull request (again, outlining the case and a
possible solution).

License
-------
MIT --- open source