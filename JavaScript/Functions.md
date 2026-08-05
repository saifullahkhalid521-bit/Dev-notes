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

# Arrow Function

An arrow function is a shorter syntax for writing functions in JavaScript.

## Example
```javascript
const add = (a, b) => {
  return a + b;
};

//for a single expression.
const add = (a, b) => a + b;

//Example
const greet = (name) => {
  console.log(`Hello, ${name}`);
};

greet("Saif");
```

arrow functions does not work like regular functions when it comes to the this keyword. It does not have its own this value, instead, it inherits this from the surrounding scope.

## Example2
```javascript
  // Global Scope

const person = {
  name: "Saif",

  greet: () => {
    console.log(this.name);
  }
};
//the above code will give undefined cause It is not inside another function.

const person = {
  name: "Saif",

  greet() {
    const showName = () => {
      console.log(this.name);
    };

    showName();
  }
};

person.greet();

//here the function will give "Saif" cause the arrow function inherits this from the surrounding scope, which is the greet method of the person object.
```
