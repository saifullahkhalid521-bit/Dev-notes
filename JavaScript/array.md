# Array

An array is a data structure that stores multiple values in a single variable, in an ordered sequence.

```javascript
let fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[0]); // Apple
```

## Array topics
* for loop in array
* forEach
* Array.from
* for...of
* for...in


### for loop in array
A for loop is used to go through each item in an array one by one and access its values.

```javascript
let fruits = ["Apple", "Banana", "Mango"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### forEach
forEach() is an array method that runs a function once for every item in the array. It gives you the current value, its index, and the original array.

```javascript
  let fruits = ["Apple", "Banana", "Mango"];

fruits.forEach(function (fruit, index, array) {
  console.log(fruit);  // Apple, Banana, Mango
  console.log(index);  // 0, 1, 2
  console.log(array);  // complete fruits array
});
```

