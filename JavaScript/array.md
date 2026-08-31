# Array

An array is a data structure that stores multiple values in a single variable, in an ordered sequence.

```javascript
let fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[0]); // Apple
```

## Array topics
* for loop in array
* forEach
* for...in
* for...of
* Array.from


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

### for...in
for...in is a JS loop used oto go through the property names (keys) of an object. It can also be used to loop through the indexes of an array.

```javascript 
for (const key in object) {
  // code to run
}
```
key is a temporary variable that holds one property name at a time.
object is the object you want to inspect.

#### Working
```javascript
 const person = {
  name: "Saif",
  age: 20,
  city: "Delhi"
};

for (const key in person) {
  console.log(key);
}
// Output:
// name
// age
// city

It gives the keys, not the values. To get the value, use square brackets:

for (const key in person) {
  console.log(key, ":", person[key]);
}

// Output:
// name : Saif
// age : 20
// city : Delhi
```

#### Working with array
```javascript
const fruits = ["apple", "banana", "mango"];

for (const index in fruits) {
  console.log(index);         // 0, 1, 2
  console.log(fruits[index]); // apple, banana, mango
}
```

### for...of
for...of loop ka use values ko one by one access karne ke liye hota hai—mostly arrays aur strings mein.

```javascript
for (const value of array) {
  // code
}
```
.value mein har turn par array ka next item aata hai.
.array woh list hai jiske items ko loop karna hai.

#### Working
```javascript
const fruits = ["apple", "banana", "mango"];

for (const fruit of fruits) {
  console.log(fruit);
}
// Output:
// apple
// banana
// mango

// Example with string
const name = "Saif";

for (const letter of name) {
  console.log(letter);
}
/*Output:
 S
/a
 i
 f */
```


## Array methods

.push() - adds one or more items to the end of an array.
.pop() - removes the last item from an array.

#### push()
Adds one or more items to the end of an array.

```javascript
let fruits = ["apple", "banana"];

fruits.push("mango");

console.log(fruits);

/*
Output:
["apple", "banana", "mango"]
*/

you can add multiple items at once:

fruits.push("orange", "grapes");
```

#### pop()
Removes the last item from an array.

```javascript
let fruits = ["apple", "banana", "mango"];

fruits.pop();

console.log(fruits);

/*
Output:
["apple", "banana"]
*/

You can also save the removed item:

let removedFruit = fruits.pop();

console.log(removedFruit); // mango
```