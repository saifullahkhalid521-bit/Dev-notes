# This and Cache
## This keywword
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

* this is not decided when the function is created.

* this is decided when the function is called.

* this does not work directly in functions.

```javascript
function greet() {
  let name = "Saif";
  console.log(this.name);
}
```
* Ye object k sath kaam karta hai , global mai variable k sath nahi kaam karta hai.
* Here this will not print "Saif" because this is not decided when the function is created. It will print undefined because this is decided when the function is called and in this case, it is called by the global object which does not have a name property.

## Cache

Cache is a concept of object that allows you to store data in memory for faster access. It is used to improve the performance of applications by reducing the time it takes to retrieve data from a slower storage medium, such as a database or an API.

### Example
```javascript
const cache = {};

function square(num) {

  if(cache[num] !== undefined){
    console.log("From Cache");
    return cache[num];
  }

  console.log("Calculated");
  const result = num * num ;

  cache[num] = result;
  return result;
}
square(5);
square(5);
square(4);
square(7);

//In the below example, shows the behavior of cache.
const threes = (num1) => {
  const cache = {};
  let count = 0;
    const two = (num2) => {
      let result = num1 + num2;
      cache[count] = result;
      count++;
      console.log(cache);
      return result;
    }
    return two;
}

const three3 = threes(5);
three3(7);
three3(4);
three3(5);
```
