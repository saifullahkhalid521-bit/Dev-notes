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

this does not work directly in functions.

```javascript
function greet() {
  let name = "Saif";
  console.log(this.name);
}
```
Here this will not print "Saif" because this is not decided when the function is created. It will print undefined because this is decided when the function is called and in this case, it is called by the global object which does not have a name property.