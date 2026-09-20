# Rest Operator
* Rest collects multiple values into a single array (or object).

## Simple Syntex
```JavaScript
function sum(...nums) {
  console.log(nums); // [1, 2, 3, 4]
  return nums.reduce((a, n) => a + n, 0);
}

sum(1, 2, 3, 4); // 10
```

### The Golder rule: Spred VS Rest
```JavaScript
const arr = [1, 2, 3];

const copy = [...arr];       // ← SPREAD (expands arr)
const [a, ...rest] = arr;    // ← REST (collects [2, 3])
```

* Memory hook:
1. Spread - spread OUT (open the box)
2. Rest - rest IN (pack the box)


## User case
1. Rest in function parameters
2. Rest with Named Params
3. Rest in Array Destructuring
4. Rest in Object Destructuring
5. Rest in Function Overloads/Variadic functions
6. Rest vs Spread in the SAME line


## 1. Rest in function parameters
```JavaScript
function sum(...nums) {
  return nums.reduce((a, n) => a + n, 0);
}
sum(1, 2, 3, 4, 5); // 15
```
* Clean, real array, works with arrows.


## 2. Rest with Named Params

* Rest collects the remaining arguments after named ones:

```javaScript
function greet(greeting, ...names) {
  return `${greeting}, ${names.join(" & ")}!`;
}

greet("Hello", "Alice", "Bob", "Charlie");
// "Hello, Alice & Bob & Charlie!"

// greeting = "Hello"

// names = ["Alice", "Bob", "Charlie"]
```
* Rule: Rest must be the LAST parameter.


## 3. Rest in Array Destructuring

```javaScript
const [first, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(rest);  // [2, 3, 4, 5]

// Skip and collect
const [, ...rest] = ["a", "b", "c", "d"];
console.log(rest); // ["b", "c", "d"]

// First + last
const [first, ...middle] = [1, 2, 3, 4, 5];
const last = middle.pop();
console.log(first, middle, last); // 1, [2, 3, 4], 5
```
* Rule: Rest must be last in the destructuring pattern too.


## 4. Rest in Object Destructuring

*Collect "everything else" from an object: 
```javaScript
const user = { name: "Alice", age: 25, city: "NYC", role: "admin" };
const { name, ...rest } = user;

console.log(name); // "Alice"
console.log(rest); // { age: 25, city: "NYC", role: "admin" }

// Real-world: Removing sensitive fields
const { password, ...safeUser } = user;
console.log(safeUser); // no password!

// React prop forwarding
function Button({ variant, ...rest }) {
  // rest = all other props
  return <button className={variant} {...rest} />;
}

// Notice the double use of ...! ...rest collects, then {...rest} spreads. Beautiful symmetry.

// Shallow copy minus a key
const obj = { a: 1, b: 2, c: 3 };
const { b, ...withoutB } = obj;
console.log(withoutB); // { a: 1, c: 3 }
```
* This is a clean way to "delete" a key without mutating. (You already saw this in the Spread lesson recap.)


## 5. Rest in Function Overloads/Variadic functions

```javaScript
function log(level, ...messages) {
  console.log(`[${level}]`, ...messages);
}

log("INFO", "Server started", "Port 3000");
// [INFO] Server started Port 3000

// Sum with minimum number of args
function sum(...nums) {
  if (nums.length === 0) return 0;
  return nums.reduce((a, n) => a + n, 0);
}

// Math utility
const max = (...nums) => Math.max(...nums);
max(1, 5, 3, 9, 2); // 9
```


## 6. Rest vs Spread in the SAME line

* You'll often see this pattern:
```javaScript
function clone(...args) {
  return [...args]; // rest collects → spread expands into new array

  // Or in React:
  function Button({ variant, ...rest }) {         // ← REST collects
  return <button className={variant} {...rest} />; // ← SPREAD expands
}
}
```
* Same line, both meanings. The position tells you which.


```javaScript
```