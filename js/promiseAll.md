# Promise.all() #

The Promise.all(iterable) method returns a single Promise that resolves when all of the promises in the iterable
argument have resolved or when the iterable argument contains no promises. 
It rejects with the reason of the first promise that rejects.

```javascript
var promise1 = Promise.resolve(3);
var promise2 = 42;
var promise3 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then(function(values) {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]

```
