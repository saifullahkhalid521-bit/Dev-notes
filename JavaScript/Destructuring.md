# Destructuring
* Destructuring is a shorthand for extracting values from arrays and objects into variables.

* Destructuring "unpack" values from arrays/objects into variables in one line.

# Types of Destructuring
1. Array destructuring   Syntax: const[a,b] = arr;  Source: Arrays(Position-based)
2. Object destructuring Synteax: const {x , y} = obj;   Source Objects (key-based)

# Array Destructuring

## Syntax
```javaScript
const nums = [10, 20, 30];
const [a, b, c] = nums;
console.log(a, b, c); // 10 20 30
```
* Position matters! a gets the first element, b gets the second, etc.

## Example
```javaScript
const nums = [10, 20, 30, 40, 50];
const [first, , third] = nums;
console.log(first, third); // 10 30
```
* The empty slot , , skips index 1.

```javaScript
let a = 1;
let b = 2;
[a, b] = [b, a];
console.log(a, b); // 2 1
```
*Classic trick — you'll see this in real code all the time.

## Rest in array destructuring
```javaScript
const [first, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(rest);  // [2, 3, 4, 5]
```
* The ...rest collects the remaining items into a new array.

## Extract from function return
```javaScript
function getCoords() {
  return [10, 20];
}

const [x, y] = getCoords();
console.log(x, y); // 10 20

// Very common with hooks like useState in React:

const [count, setCount] = useState(0);
```

## Array Destructuring Gotchas
1. Order matters
```javaScript
const [a, b] = [1, 2];  // a=1, b=2
const [b, a] = [1, 2];  // b=1, a=2  ← different!
```

2. Missing elements
```javaScript
const [a, b, c] = [1, 2];
console.log(c); // undefined
```

3. null doesn't trigger defaults
```javaScript
const [a = 5] = [null];
console.log(a); // null (not 5)
```

4. Swapping needs semicolons (in some cases)
 ```javaScript
 let a = 1, b = 2;
[a, b] = [b, a];  // works
```
* But if the previous line ends without a semicolon, JS might interpret [a, b] as an index access. Always use semicolons or add one on the previous line.


 ```javaScript
```