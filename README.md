# menrva

<!-- README.md is autogenerated -->

[![Build Status](https://secure.travis-ci.org/phadej/menrva.svg?branch=master)](http://travis-ci.org/phadej/menrva)
[![NPM version](http://img.shields.io/npm/v/menrva.svg)](https://www.npmjs.org/package/menrva)
[![Dependency Status](https://david-dm.org/phadej/menrva.svg)](https://david-dm.org/phadej/menrva)
[![devDependency Status](https://david-dm.org/phadej/menrva/dev-status.svg)](https://david-dm.org/phadej/menrva#info=devDependencies)
[![Coverage Status](https://img.shields.io/coveralls/phadej/menrva.svg)](https://coveralls.io/r/phadej/menrva?branch=master)
[![Code Climate](http://img.shields.io/codeclimate/github/phadej/menrva.svg)](https://codeclimate.com/github/phadej/menrva)

Ambitious data-flow library.

## Getting Started
Install the module with: `npm install menrva`

```js
var menrva = require('menrva');
menrva.some('awe'); // some, as in awesome?
```

## API


### Equalities

#### egal

> egal (a, b) : boolean

Identity check. `Object.is`. http://wiki.ecmascript.org/doku.php?id=harmony:egal



### Option

Also known as `Maybe`.


#### option.equals

> equals (@ : option a, other : *, eq = eqal : a -> a -> boolean) : boolean

Equality check.


#### option.map

> map (@ : option a, f : a -> b) : option b


#### option.elim

> elim (@ : option a, x : b, f : a -> b) : b



#### option.orElse

> orElse (@ : option a, x : a) : a



### Signal

The core type of menrva. `Signal` is abstract class, and cannot be created explicitly.

Similar concepts are: *Behaviours* in FRP, *Properties* in bacon.js.


#### signal.map

> map (@ : Signal a, f : a -> b, eq = egal : b -> b -> boolean) : Signal b


#### signal.onValue

> onValue (@ : Singal a, callback : a -> void) -> Unsubscriber

Add value callback. `callback` is immediately executed with the current value of signal.
After than `callback` will be called, each time signal's value changes.

The return value is a function, which will remove the callback if executed.


### Source

A signal which value you can set.

Similar concepts are: *Bacon.Model* in bacon.js, *BehaviourSubject* in Rx.


#### new Source

> new Source (initialValue : a, eq = egal : a -> a -> boolean) : Source a


#### source.set

> set (@ : Source a, tx : Transaction, value : a) : void


#### source.modify

> modify (@ : Source a, tx : Transaction, f : a -> a) : void

Mofify source value. `f` will be called with current value of signal inside the transaction.


### Signal combinators


#### combine

> combine (Signal a..., f : a... -> b) : Signal b

Applicative n-ary lift.



### Transaction

One gathers atomic updates into single transaction (to avoid glitches).

```js
var tx = new Transaction();
sourceA.set(tx, 42);
sourceB.set(tx, "foobar");
tx.commit(); // not necessary, transactions are auto-commited
```


#### transaction.commit

Commit the transaction, forcing synchronous data propagation.


#### transaction.rollback

Rollback the transaction. Maybe be called multiple times (consecutives calls are no-op).

*Note: for now `rollback` only resets the pending actions in transactions. Transaction is still valid, and more actions can be added*



## Contributing


In lieu of a formal styleguide, take care to maintain the existing coding style.

Add tests for any new or changed functionality. 100% coverage isn't hard. Semantic coverage is important too though.

Note: `README.md` is autogenerated file.

## Release History


- **0.0.1** Name reservation

## License

Copyright (c) 2014 Oleg Grenrus.
Licensed under the MIT license.
