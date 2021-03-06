[![npm](https://img.shields.io/npm/v/@smockle/safe.svg)](https://www.npmjs.com/package/@smockle/safe)
[![Build Status](https://travis-ci.org/smockle/safe.svg?branch=master)](https://travis-ci.org/smockle/safe)
[![Build status](https://ci.appveyor.com/api/projects/status/x1sjhd5q1jv1eupd?svg=true)](https://ci.appveyor.com/project/smockle/safe)
[![codecov](https://codecov.io/gh/smockle/safe/branch/master/graph/badge.svg)](https://codecov.io/gh/smockle/safe)
[![Known Vulnerabilities](https://snyk.io/test/github/smockle/safe/badge.svg)](https://snyk.io/test/github/smockle/safe)
[![Greenkeeper badge](https://badges.greenkeeper.io/smockle/safe.svg)](https://greenkeeper.io/)

# safe

Verifies argument types.

## Installation

Run `npm install --save @smockle/safe` to add `safe` to your project.

## Usage

`safe` can be called within a function to verify argument types:

```JavaScript
const safe = require('./lib/safe').safe

function toUpperAndNotEmpty (xs, x) {
  const unsafe = safe([
    { name: 'xs', type: 'array' },
    { name: 'x', type: 'string' }
  ], arguments)
  if (unsafe) throw unsafe
  return xs.concat(x ? x.toUpperCase() : [])
}

const a = [ 'aaa', 222, '', 'ccc', '' ]
a.reduce(toUpperAndNotEmpty, [])
// Throws TypeError('x must be a string')

const b = [ 'aaa', 'bbb', '', 'ccc', '' ]
b.reduce(toUpperAndNotEmpty, [])
// [ 'AAA', 'BBB', 'CCC' ]
```

`safe` also includes a wrapper that accepts functions as a callback:

```JavaScript
const safe = require('./lib/wrapper').safe

const toUpperAndNotEmpty = safe([
  { name: 'xs', type: 'array' },
  { name: 'x', type: 'string' }
])(
  function (xs, x) {
    return xs.concat(x ? x.toUpperCase() : [])
  }
)

const a = [ 'aaa', 222, '', 'ccc', '' ]
a.reduce(toUpperAndNotEmpty, [])
// Throws TypeError('x must be a string')

const b = [ 'aaa', 'bbb', '', 'ccc', '' ]
b.reduce(toUpperAndNotEmpty, [])
// [ 'AAA', 'BBB', 'CCC' ]
```

## API Reference

* [safe](#module_safe)
    * [.IDENTITY](#module_safe.IDENTITY) : <code>Object.&lt;string, string&gt;</code>
    * [.identifyTypeClass(type)](#module_safe.identifyTypeClass) ⇒ <code>string</code> \| <code>null</code>
    * [.isSafe(type, value)](#module_safe.isSafe) ⇒ <code>Boolean</code>
    * [.safe(types, value)](#module_safe.safe) ⇒ <code>TypeError</code>

<a name="module_safe.IDENTITY"></a>

### safe.IDENTITY : <code>Object.&lt;string, string&gt;</code>
Dictionary of type classes.

**Kind**: static constant of [<code>safe</code>](#module_safe)  
<a name="module_safe.identifyTypeClass"></a>

### safe.identifyTypeClass(type) ⇒ <code>string</code> \| <code>null</code>
Select type class matching the provided parameter.

**Kind**: static method of [<code>safe</code>](#module_safe)  
**Returns**: <code>string</code> \| <code>null</code> - Type class.  

| Param | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | String representation of a primitive or instantiable type. |

<a name="module_safe.isSafe"></a>

### safe.isSafe(type, value) ⇒ <code>Boolean</code>
Whether value is of provided type.

**Kind**: static method of [<code>safe</code>](#module_safe)  
**Returns**: <code>Boolean</code> - Value is of provided type.  

| Param | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | String representation of a primitive or instantiable type. |
| value | <code>\*</code> | Value to check. |

<a name="module_safe.safe"></a>

### safe.safe(types, value) ⇒ <code>TypeError</code>
Create TypeError when an argument doesn’t match provided type.

**Kind**: static method of [<code>safe</code>](#module_safe)  
**Returns**: <code>TypeError</code> - Argument doesn’t match provided type.  

| Param | Type | Description |
| --- | --- | --- |
| types | <code>Array.&lt;Object.&lt;string, string&gt;&gt;</code> | List of parameter names and types. |
| value | <code>\*</code> | List of values to check. |


ERROR, Cannot find module.

* [instantiable](#module_instantiable)
    * [.instantiables](#module_instantiable.instantiables) : <code>Object.&lt;string, (function()\|Object\|number)&gt;</code>
    * [.instantiableKeys](#module_instantiable.instantiableKeys) : <code>Array.&lt;string&gt;</code>
    * [.isInstantiable(type)](#module_instantiable.isInstantiable) ⇒ <code>Boolean</code>
    * [.instanceOf(type, value)](#module_instantiable.instanceOf) ⇒ <code>Boolean</code>

<a name="module_instantiable.instantiables"></a>

### instantiable.instantiables : <code>Object.&lt;string, (function()\|Object\|number)&gt;</code>
Dictionary of instantiable names to instantiable types.

**Kind**: static constant of [<code>instantiable</code>](#module_instantiable)  
<a name="module_instantiable.instantiableKeys"></a>

### instantiable.instantiableKeys : <code>Array.&lt;string&gt;</code>
List of instantiable types.

**Kind**: static constant of [<code>instantiable</code>](#module_instantiable)  
<a name="module_instantiable.isInstantiable"></a>

### instantiable.isInstantiable(type) ⇒ <code>Boolean</code>
Whether parameter represents an instantiable type.

**Kind**: static method of [<code>instantiable</code>](#module_instantiable)  
**Returns**: <code>Boolean</code> - Parameter represents an instantiable type.  

| Param | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | String representation of an instantiable type. |

<a name="module_instantiable.instanceOf"></a>

### instantiable.instanceOf(type, value) ⇒ <code>Boolean</code>
Whether value is of provided instantiable type.

**Kind**: static method of [<code>instantiable</code>](#module_instantiable)  
**Returns**: <code>Boolean</code> - Value is of provided instantiable type.  

| Param | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | String representation of a instantiable type. |
| value | <code>\*</code> | Value to check. |


## Testing

`safe` includes several unit tests. After cloning the `safe` repo locally, run `npm install` in the project folder to install dependencies. Run `npm test` to execute the tests.
