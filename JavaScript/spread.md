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


3. Passing array items as function arguments
```javaScript
const nums = [1, 2, 3];
console.log(...nums); // 1 2 3 — same as console.log(1, 2, 3)
```
* This is how Math.max(...arr) works — you already used this in the sort lesson.


4. Spreaqding Strings

```javaScript
const word = "hello";
const chars = [...word];
console.log(chars); // ["h", "e", "l", "l", "o"]

const reversed = [...word].reverse().join("");
console.log(reversed); // "olleh"
```
* Strings are iterable, so you can spread them:


5. Converting Iterables to arrays

```javaScript
const set = new Set([1, 2, 2, 3, 3]);
const arr = [...set];
console.log(arr); // [1, 2, 3]

const map = new Map([["a", 1], ["b", 2]]);
console.log([...map]); // [["a", 1], ["b", 2]]
```


6. Adding Elements

1. Add to end
```javaScript
const arr = [1, 2, 3];
const withEnd = [...arr, 4];
// [1, 2, 3, 4]
```

2. Add to beginnig
```javaScript
const withStart = [0, ...arr];
// [0, 1, 2, 3]
```

3. Add to middle
```javaScript
const mid = [...arr.slice(0, 1), 99, ...arr.slice(1)];
// [1, 99, 2, 3]
```
* Why not just push? Because spread gives you a new array instead of mutating. In React (immutability), this matters.



```javaScript

```