## Scope
... in JS defines what variables you have access to. There are two kinds of scope - global and local.

### Global Scope
Variable is defined in the `global scope` if is declared outside of all functions or outside curly bracecs { }.

```js
  const global = "This primitive string is availible in global scope"
```
Variable declared in `global scope` can be used anywhere in code, even inside functions like in example below, but it is not advised.
This is because with declaring global variables is a chance of naming collisions or if U using var second variable with the same name overwrites first one after it is declared. 
```js 
  const globalVar = "hi!"
  
  function sayHello () {
    console.log(globalVar)
  }
  
  console.log(globalVar)
  sayHello() // we should received 2 consol logs with "hi!"
```
```js 
  // Don't do this!
let thing = 'something'
let thing = 'something else' // Error, thing has already been declared
```
```js 
  // Don't do this!
var thing = 'something'
var thing = 'something else' // perhaps somewhere totally different in your code
console.log(thing) // 'something else'
```

### Local scope
In JS there are two kinds of local scope:
- function scope
- block scope

#### Function scope
When you declare a variable inside a function, you have acces to this variable only inside that function. 
```js
function local () {
  const inner = "workin only inside"
  console.log(inner) // here we can see inner 
}

console.log(inner) // on console.log call we get an error, because inner is not defined in this place
```
### Block scope
When you declare a variable with `const` or `let` within `{ }`, you can acces these variables only within `{ }`.

```js
  {
  const hello = 'Hello CSS-Tricks Reader!'
  console.log(hello) // 'Hello CSS-Tricks Reader!'
}

console.log(hello) // Error, hello is not defined
```
The block scope is a subset of a function scope since functions need to be declared with curly braces (unless you're using arrow functions with an implicit return).
