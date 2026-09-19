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


## Gotchas to Remember

1. Spread Creates a SHALLOW copy

```javaScript
const user = { name: "Alice", address: { city: "NYC" } };
const copy = { ...user };

copy.address.city = "LA";
console.log(user.address.city); // "LA" — nested object was NOT copied!

To Deep Copy use structuredClone()

example
const userProfile = {
  id: 101,
  info: {
    name: "Alex",
    preferences: {
      theme: "dark",
      notifications: true
    }}};
const userProfileDeepCopy = structuredClone(userProfile);
userProfileDeepCopy.info.preferences.theme = 'Light';
console.log(userProfileDeepCopy);
```
* Nested objects/arrays still share the same reference. For deep copies, use structuredClone() (modern) or a library.


2. Spread Vs Rest - same ... , opposite roles

```javaScript
const [a, ...rest] = arr;       // ← REST (collects)
const arr2 = [...arr];           // ← SPREAD (expands)
```


3. Can't spread non-iterables

```javaScript
const obj = { a: 1 };
console.log(...obj); // ❌ TypeError: obj is not iterable

const nums = 5;
console.log(...nums); // ❌ TypeError

But — objects can be spread inside another object:

const copy = { ...obj }; // ✅ works (object spread is a special case)
```


4. null/undefined inside spread → no error

```javaScript
const a = [1, 2];
const b = null;
const result = [...a, ...(b || [])]; // ✅
console.log([...a, ...[]]); // ✅ [1, 2]

// Actually, spreading null/undefined in object spread is safe:
{ ...null } // {} (no error)
{ ...undefined } // {}

// But spreading null in an array context is an error:
[null] // [null] ✅
[...null] // ❌ TypeError
```

5. Spread doesn't spread objects into arrays

```javaScript
const obj = { a: 1, b: 2 };
[...obj] // ❌ TypeError — object is not iterable

// But this works (extracts values):
Object.values(obj); // [1, 2]

// Or keys:
[...Object.keys(obj)]; // ["a", "b"]
```


6. Performance

* For very large arrays, slice() might be faster than [...arr]. But in 99% of code, spread is fine and more readable.



## The "Spread + Immutability" Pattern (Memorize)
```javaScript
// Array — add
const newArr = [...arr, item];

// Array — remove by index
const newArr = [...arr.slice(0, i), ...arr.slice(i + 1)];

// Array — update by index
const newArr = arr.map((x, idx) => idx === i ? newVal : x);

// Object — update
const newObj = { ...obj, key: newVal };

// Object — delete
const { keyToRemove, ...rest } = obj;
```