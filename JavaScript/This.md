# This keywword
this is a keyword that refers to the object that calls the function.

```javascript
    const person1 = {
  name: "Saif",

  greet() {
    console.log(this.name);
  }
};

const person2 = {
  name: "Ali"
};

person2.greet = person1.greet;

person2.greet();
```

this is not decided when the function is created.

this is decided when the function is called.