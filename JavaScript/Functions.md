# Declaration Funciton

It's a way to define a function using the function keyword. It is hoisted, which means you can call it before it is written in your code.

## Example
```javascript
greet(); // Works

function greet() {
  console.log("Hello!");
}
```

# Function Expression

It's a function that is assigned to a variable. Unlike a function declaration, it cannot be called before it is defined because only the variable is hoisted, not its value.

## Example
```javascript
const greet = function () {
  console.log("Hello!");
};

greet();
```