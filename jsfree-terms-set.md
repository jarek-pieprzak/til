### temporal dead zone - where you cannot access variable before it is defined

```js
  var pizza = 'Deep Dish 🍕🍕🍕';
console.log(pizza); // -> returns pizza value

console.log(pizza); // -> returns `undefined` because identifier pizza is not bound with value at this moment
var pizza = 'Deep Dish 🍕🍕🍕';

```
