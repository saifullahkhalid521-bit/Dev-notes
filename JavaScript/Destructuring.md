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

___________________________________________________________________________________________________________________________________________________________

# Objest Destructuring
## Syntax
 ```javaScript
 const user = { name: "Alice", age: 25, city: "NYC" };
const { name, age } = user;
console.log(name, age); // "Alice" 25

// * Key name matters, not position!

const { age, name } = user; // still works — order doesn't matter
```

## Rename variables
 ```javaScript
 const user = { name: "Alice", age: 25 };
const { name: userName, age: userAge } = user;
console.log(userName, userAge); // "Alice" 25
```
* Syntax: { originalKey: newVariableName }
* Very useful when key names are too generic.


## Combine rename + default
 ```javaScript
 const user = { name: "Alice" };
// Destructuring step-by-step:
const { 
  name: userName = "Guest", // user.name is "Alice" -> Default skipped -> userName = "Alice"
  age: userAge = 0          // user.age is undefined -> Default triggered -> userAge = 0
} = user;
```
* When you destructure an object property:

* Property exists and is NOT undefined: JavaScript uses the actual value from the object.

* Property is missing OR strictly undefined: JavaScript falls back to the default value you provided.


## Destructure nested objects
 ```javaScript
 const user = {
  name: "Alice",
  address: {
    city: "NYC",
    zip: "10001"
  }
};

const { address: { city, zip } } = user;
console.log(city, zip); // "NYC" "10001"

// You can go as deep as you need
const { address: { city: userCity } } = user;
```

## Destructure in function parameters
 ```javaScript
 //Without destructuring
 function greet(user) {
  console.log(`Hello, ${user.name} from ${user.city}`);
}
greet({ name: "Alice", city: "NYC" });

//With destructuring
function greet({ name, city }) {
  console.log(`Hello, ${name} from ${city}`);
}
greet({ name: "Alice", city: "NYC" });
//Cleaner, self-documenting.

//With defaults
function greet({ name = "Guest", city = "Nowhere" } = {}) {console.log(`Hello, ${name} from ${city}`);}
greet(); // "Hello, Guest from Nowhere"

// The = {} at the end is important — it ensures the function doesn't crash if called with no argument.
```


## Rest in object destructuring
 ```javaScript
const user = { name: "Alice", age: 25, city: "NYC", role: "admin" };
const { name, ...rest } = user;
console.log(name);  // "Alice"
console.log(rest);  // { age: 25, city: "NYC", role: "admin" }
```
* Very common in React for passing props:
 ```javaScript
 function Button({ onClick, ...rest }) {
  // rest contains all other props
}
```

## Destructure props inReact (real-world)
 ```javaScript
 // Without destructuring
function UserCard(props) {
  return <div>{props.name} ({props.age})</div>;
}

// With destructuring (preferred)
function UserCard({ name, age }) {
  return <div>{name} ({age})</div>;
}
```
* This is the reason destructuring is essential for React.

## Common Gotchas

1. Forgetting parentheses when destructuring let/const from a value
```javascript
const user = { name: "Alice" };
const { name } = user;      // ✅
const { name } = getuser(); // ✅

let { name } = user;         // ✅
// { name } = user;          // ❌ syntax error — need parens
({ name } = user);           // ✅
```

2. Destructuring from null/undefined crashes
```javascript
const { name } = null;       // ❌ TypeError
const { name } = undefined;  // ❌ TypeError
const { name } = {};         // ✅ undefined
```

3. defaultValue only for undefined, not null
```javascript
const { a = 1 } = { a: null };
console.log(a); // null (not 1)
```

4. Nested destructuring crashes if parent is missing
```javascript
const user = {};
const { address: { city } } = user; // ❌ TypeError

// Fix with defaults:

const { address: { city } = {} } = user;
console.log(city); // undefined — no crash
```

5. Don't confuse destructuring with object literal
```javascript
const { a } = obj;   // ✅ destructuring — extracts a from obj
const { a } = { a: 1 }; // ✅ destructuring with literal on right
const obj2 = { a };  // ✅ shorthand — creates { a: a }
```
* Look at the left side: { a } = destructure. Right side: { a } = shorthand property.

 ```javaScript
```