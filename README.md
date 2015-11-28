foo

# API Reference
<a name="Injector"></a>
## Injector
**Kind**: global class  

* [Injector](#Injector)
  * [new Injector([nameMaker])](#new_Injector_new)
  * _instance_
    * [.register(name, fn)](#Injector+register)
    * [.registerValue(name, value)](#Injector+registerValue)
    * [.registerPath(patterns, [globOptions])](#Injector+registerPath)
    * [.registerRequires(reqs, [mod])](#Injector+registerRequires) ⇒ <code>[Injector](#Injector)</code>
    * [.resolve(names)](#Injector+resolve) ⇒ <code>\*</code> &#124; <code>Array.&lt;\*&gt;</code>
    * [.resolve(fn, [locals])](#Injector+resolve) ⇒ <code>\*</code>
    * [.resolvePath(p, [locals])](#Injector+resolvePath) ⇒ <code>\*</code>
  * _inner_
    * [~nameMakerCallback](#Injector..nameMakerCallback) : <code>function</code>

<a name="new_Injector_new"></a>
### new Injector([nameMaker])
Initializes a new Injector.


| Param | Type | Description |
| --- | --- | --- |
| [nameMaker] | <code>[nameMakerCallback](#Injector..nameMakerCallback)</code> | A function that creates a name for a module registered by path. |

**Example**  
```js
var injector = new Injector();
```
**Example**  
```js
var injector = new Injector(function (basename, realpath, fn) {
```
<a name="Injector+register"></a>
### injector.register(name, fn)
Register a module.

**Kind**: instance method of <code>[Injector](#Injector)</code>  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | Name of the module. |
| fn | <code>function</code> | A module function to register. |

**Example**  
```js
injector.register("foo", function (dependencyA, dependencyB) {
```
<a name="Injector+registerValue"></a>
### injector.registerValue(name, value)
Register a fixed value. (This is syntactic sugar for registering a function that simply returns the given value.)

**Kind**: instance method of <code>[Injector](#Injector)</code>  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | The name of the module. |
| value | <code>\*</code> | The value to register. |

**Example**  
```js
// Register the value 5 with the name "foo".
```
**Example**  
```js
// Register a function with the name "doubler".
```
<a name="Injector+registerPath"></a>
### injector.registerPath(patterns, [globOptions])
Register module(s) with the given path pattern(s).

**Kind**: instance method of <code>[Injector](#Injector)</code>  

| Param | Type | Description |
| --- | --- | --- |
| patterns | <code>string</code> &#124; <code>Array.&lt;string&gt;</code> | The pattern or patterns to match. This uses the [glob-all](https://github.com/jpillora/node-glob-all) module, which accepts negative patterns as well. |
| [globOptions] | <code>Object</code> | Options to pass to [glob-all](https://github.com/jpillora/node-glob-all) and, in turn, [glob](https://github.com/isaacs/node-glob). |

**Example**  
```js
// Register a single file.
```
**Example**  
```js
// Register all JS files except spec files.
```
<a name="Injector+registerRequires"></a>
### injector.registerRequires(reqs, [mod]) ⇒ <code>[Injector](#Injector)</code>
Requires modules and registers them with the name provided.

**Kind**: instance method of <code>[Injector](#Injector)</code>  
**Returns**: <code>[Injector](#Injector)</code> - The injector (for chaining).  

| Param | Type | Description |
| --- | --- | --- |
| reqs | <code>Object.&lt;string, string&gt;</code> | Object with keys as injector names and values as module names to require. |
| [mod] | <code>Module</code> | The module to run [require](https://nodejs.org/api/modules.html#modules_module_require_id) on. Defaults to the Injector module, which should typically behave correctly. |

**Example**  
```js
injector.registerRequires({
```
<a name="Injector+resolve"></a>
### injector.resolve(names) ⇒ <code>\*</code> &#124; <code>Array.&lt;\*&gt;</code>
Resolve a module or multiple modules.

**Kind**: instance method of <code>[Injector](#Injector)</code>  
**Returns**: <code>\*</code> &#124; <code>Array.&lt;\*&gt;</code> - The resolved value(s).  

| Param | Type | Description |
| --- | --- | --- |
| names | <code>string</code> &#124; <code>Array.&lt;string&gt;</code> | Name or names to resolve. |

**Example**  
```js
var log = injector.resolve("log");
```
**Example**  
```js
var resolved = injector.resolve(["fs", "log"]);
```
<a name="Injector+resolve"></a>
### injector.resolve(fn, [locals]) ⇒ <code>\*</code>
Resolve a module or multiple modules.

**Kind**: instance method of <code>[Injector](#Injector)</code>  
**Returns**: <code>\*</code> - The result of the executed function.  

| Param | Type | Description |
| --- | --- | --- |
| fn | <code>function</code> | Function to execute. |
| [locals] | <code>Object.&lt;string, \*&gt;</code> | Local variables to inject into the function. |

**Example**  
```js
// Resolve someNum and otherNum and set the result to the sum.
```
**Example**  
```js
// This is essentially the same thing using a return in the function.
```
**Example**  
```js
// You can also provide or override dependencies using the locals argument.
```
<a name="Injector+resolvePath"></a>
### injector.resolvePath(p, [locals]) ⇒ <code>\*</code>
Resolve a module with the given path.

**Kind**: instance method of <code>[Injector](#Injector)</code>  
**Returns**: <code>\*</code> - The result of the executed function.  

| Param | Type | Description |
| --- | --- | --- |
| p | <code>string</code> | The path to resolve. |
| [locals] | <code>Object.&lt;string, \*&gt;</code> | Local variables to inject into the function. |

**Example**  
```js
var log = injector.resolvePath("path/to/log.js");
```
<a name="Injector..nameMakerCallback"></a>
### Injector~nameMakerCallback : <code>function</code>
A function that creates a name for a module registered by path.

**Kind**: inner typedef of <code>[Injector](#Injector)</code>  

| Param | Type | Description |
| --- | --- | --- |
| basename | <code>string</code> | The basename of the loaded module. |
| realpath | <code>string</code> | The full path of the loaded module. |
| fn | <code>function</code> | The actual module factory function. |
