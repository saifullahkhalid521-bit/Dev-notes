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










```javaScript
```