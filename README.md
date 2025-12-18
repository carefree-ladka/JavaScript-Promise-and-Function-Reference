# JavaScript Promise and Function Reference

## Table of Contents

- [Promise](#promise)
  - [Constructor](#constructor)
    - [Promise()](#promise-1)
  - [Static Methods](#static-methods)
    - [Promise.all()](#promiseall)
    - [Promise.allSettled()](#promiseallsettled)
    - [Promise.any()](#promiseany)
    - [Promise.race()](#promiserace)
    - [Promise.reject()](#promisereject)
    - [Promise.resolve()](#promiseresolve)
    - [Promise.try()](#promisetry)
    - [Promise.withResolvers()](#promisewithresolvers)
  - [Static Properties](#static-properties)
    - [Promise[Symbol.species]](#promisesymbolspecies)
  - [Instance Methods](#instance-methods)
    - [catch()](#catch)
    - [finally()](#finally)
    - [then()](#then)
- [Function](#function)
  - [Inheritance](#inheritance)
  - [Static Methods](#static-methods-1)
    - [Function.apply()](#functionapply)
    - [Function.bind()](#functionbind)
    - [Function.call()](#functioncall)
    - [Function.toString()](#functiontostring)
    - [Function[Symbol.hasInstance]()](#functionsymbolhasinstance)
  - [Static Properties](#static-properties-1)
    - [Function.length](#functionlength)
    - [Function.name](#functionname)
    - [Function.prototype](#functionprototype)
  - [Instance Methods](#instance-methods-1)
    - [apply()](#apply)
    - [bind()](#bind)
    - [call()](#call)
    - [toString()](#tostring)
    - [Symbol.hasInstance()](#symbolhasinstance)
  - [Instance Properties](#instance-properties)
    - [arguments](#arguments)
    - [caller](#caller)
    - [displayName](#displayname)
    - [length](#length)
    - [name](#name)
    - [prototype](#prototype)

---

## Promise

The `Promise` object represents the eventual completion or failure of an asynchronous operation and its resulting value. A Promise is a proxy for a value not necessarily known when the promise is created, allowing you to associate handlers with an asynchronous action's eventual success value or failure reason.

### Constructor

#### Promise()

Creates a new Promise object. The constructor is primarily used to wrap functions that do not already support promises.

**Syntax:**
```javascript
new Promise(executor)
```

**Parameters:**
- `executor`: A function with two parameters `resolve` and `reject`

**Example:**
```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve('Success!'), 1000);
});
```

### Static Methods

#### Promise.all()

Takes an iterable of promises and returns a single Promise that resolves when all of the input promises have resolved, or rejects when any input promise rejects.

**Syntax:**
```javascript
Promise.all(iterable)
```

**Example:**
```javascript
Promise.all([promise1, promise2, promise3])
  .then(values => console.log(values));
```

#### Promise.allSettled()

Returns a promise that resolves after all of the given promises have either resolved or rejected, with an array of objects describing the outcome of each promise.

**Syntax:**
```javascript
Promise.allSettled(iterable)
```

**Example:**
```javascript
Promise.allSettled([promise1, promise2])
  .then(results => results.forEach(result => console.log(result.status)));
```

#### Promise.any()

Takes an iterable of promises and returns a single promise that resolves as soon as any of the input promises resolves. It rejects when all input promises reject.

**Syntax:**
```javascript
Promise.any(iterable)
```

**Example:**
```javascript
Promise.any([promise1, promise2, promise3])
  .then(value => console.log(value))
  .catch(error => console.error(error));
```

#### Promise.race()

Returns a promise that fulfills or rejects as soon as one of the input promises fulfills or rejects, with the value or reason from that promise.

**Syntax:**
```javascript
Promise.race(iterable)
```

**Example:**
```javascript
Promise.race([promise1, promise2])
  .then(value => console.log(value));
```

#### Promise.reject()

Returns a Promise object that is rejected with a given reason.

**Syntax:**
```javascript
Promise.reject(reason)
```

**Example:**
```javascript
Promise.reject(new Error('Failed'))
  .catch(error => console.error(error));
```

#### Promise.resolve()

Returns a Promise object that is resolved with a given value. If the value is a thenable, the returned promise will follow that thenable.

**Syntax:**
```javascript
Promise.resolve(value)
```

**Example:**
```javascript
Promise.resolve('Success')
  .then(value => console.log(value));
```

#### Promise.try()

Takes a callback of any kind (returns or throws, synchronously or asynchronously) and wraps its result in a Promise.

**Syntax:**
```javascript
Promise.try(func)
```

**Example:**
```javascript
Promise.try(() => riskyOperation())
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

#### Promise.withResolvers()

Returns an object containing a new Promise object and two functions to resolve or reject it, corresponding to the two parameters passed to the executor of the Promise constructor.

**Syntax:**
```javascript
Promise.withResolvers()
```

**Example:**
```javascript
const { promise, resolve, reject } = Promise.withResolvers();
// Use resolve() or reject() later
```

### Static Properties

#### Promise[Symbol.species]

Returns the constructor used to construct return values from promise methods.

### Instance Methods

#### catch()

Appends a rejection handler callback to the promise and returns a new promise resolving to the return value of the callback if it is called, or to its original fulfillment value if the promise is instead fulfilled.

**Syntax:**
```javascript
promise.catch(onRejected)
```

**Example:**
```javascript
promise.catch(error => {
  console.error('Error:', error);
});
```

#### finally()

Appends a handler to the promise and returns a new promise that is resolved when the original promise is resolved. The handler is called when the promise is settled, whether fulfilled or rejected.

**Syntax:**
```javascript
promise.finally(onFinally)
```

**Example:**
```javascript
promise.finally(() => {
  console.log('Promise settled');
});
```

#### then()

Appends fulfillment and rejection handlers to the promise and returns a new promise resolving to the return value of the called handler.

**Syntax:**
```javascript
promise.then(onFulfilled, onRejected)
```

**Example:**
```javascript
promise.then(
  value => console.log('Success:', value),
  error => console.error('Error:', error)
);
```

---

## Function

Every JavaScript function is actually a Function object. The Function constructor creates a new Function object, but calling it directly can create functions dynamically which can be a security risk.

### Inheritance

Function inherits from Object, meaning it has access to all Object methods and properties.

### Static Methods

#### Function.apply()

Calls a function with a given `this` value and arguments provided as an array.

**Syntax:**
```javascript
func.apply(thisArg, argsArray)
```

**Example:**
```javascript
Math.max.apply(null, [1, 2, 3]); // 3
```

#### Function.bind()

Creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

**Syntax:**
```javascript
func.bind(thisArg, arg1, arg2, ...)
```

**Example:**
```javascript
const boundFunc = func.bind(obj, arg1);
boundFunc(arg2);
```

#### Function.call()

Calls a function with a given `this` value and arguments provided individually.

**Syntax:**
```javascript
func.call(thisArg, arg1, arg2, ...)
```

**Example:**
```javascript
func.call(obj, 'arg1', 'arg2');
```

#### Function.toString()

Returns a string representing the source code of the function.

**Syntax:**
```javascript
func.toString()
```

**Example:**
```javascript
function sum(a, b) { return a + b; }
console.log(sum.toString());
// "function sum(a, b) { return a + b; }"
```

#### Function[Symbol.hasInstance]()

Determines if a constructor object recognizes an object as one of the constructor's instances.

**Syntax:**
```javascript
func[Symbol.hasInstance](instance)
```

### Static Properties

#### Function.length

Specifies the number of arguments expected by the function.

#### Function.name

The name of the function.

#### Function.prototype

The Function prototype object.

### Instance Methods

#### apply()

Calls a function with a given `this` value and arguments provided as an array (or array-like object).

#### bind()

Creates a new function with a specified `this` value and optional initial arguments.

#### call()

Calls a function with a given `this` value and individual arguments.

#### toString()

Returns a string representation of the function's source code.

#### Symbol.hasInstance()

Method used to determine if an object is an instance of this function.

### Instance Properties

#### arguments

An array-like object containing the arguments passed to the function (deprecated in strict mode).

#### caller

Specifies the function that invoked the currently executing function (deprecated).

#### displayName

An optional name for the function used in debuggers and error stack traces.

#### length

The number of parameters expected by the function.

#### name

The name of the function.

#### prototype

Used when the function is used as a constructor with the `new` operator. It will become the new object's prototype.

---

## Additional Resources

For more detailed information and examples, visit the [MDN Web Docs](https://developer.mozilla.org/).

## License

This content is derived from MDN Web Docs and is available under a Creative Commons license.
