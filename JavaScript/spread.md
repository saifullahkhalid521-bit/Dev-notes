# Spread Operator

* The spread operator expands an iterable (array, string, object) into individual elements.

## Used in
1. Copying arrays/objects
2. Merging arrays/objects
3. Passing array items as function arguments
4. Converting iterables to arrays

## Basic Syntax
```javaScript
const arr = [1, 2, 3];
console.log(...arr); // 1 2 3  (not [1, 2, 3] — three separate values!)
```

* The Core Mental Model

```javaScript
const nums = [1, 2, 3];

// Without spread
console.log(nums);   // [1, 2, 3]  (one array)

// With spread
console.log(...nums); // 1 2 3     (three separate values)
```

## Use Cases

1. Copying Arrays and Objects

```javaScript
//With array
const a = [1, 2, 3];
const b = [...a];     // ✅ shallow copy
b.push(4);
console.log(a);       // [1, 2, 3] — untouched
console.log(b);       // [1, 2, 3, 4]

//With object
const copy = { ...user };
copy.age = 30;
console.log(user.age); // 25 — untouched

```
* it creates a real copy of array 


2. Merging Arrays and Objects

```javaScript
// With arrays

const merged = [...a, ...b];
console.log(merged); // [1, 2, 3, 4]

//Insert in the middle
const result = [...a, 99, ...b];
console.log(result); // [1, 2, 99, 3, 4]


//With Objects

const merged = { ...a, ...b };
console.log(merged); // { x: 1, y: 3, z: 4 }
// Order matters — later keys override earlier ones

const user = { name: "Alice", age: 25, city: "NYC" };
const updated = { ...user, age: 30 };
console.log(updated); // { name: "Alice", age: 30, city: "NYC" }
// The age from the last spread wins. This is how React state updates work.
```
