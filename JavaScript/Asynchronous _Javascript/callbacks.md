# Callbacks

Callbacks ek function hai jo dusre function ke andar argument ke roop me pass hota hai. Callback function ko dusre function ke andar call kiya jata hai.

* Used to handle asynchronous operations in JavaScript.

* Reading a file
* Network requests
* Interacting with databases

## Syntax
```javascript
  function greet(name , callback){
  console.log(`Hello, ${name}`);
  callback();
}

function afterGreeting(){
  console.log("Greeting complete!");
}

greet("Saif" , afterGreeting);
```



### Example

```javascript

//Order Food
function orderFood(food , callback){
  console.log(`${food} order ho raha hai...`);

  setTimeout(()=> {
    callback(food);
  }, 2000);
}

function readyFood(food) {
  console.log(`${food} ready hai!`);
}

orderFood('Pizza' , readyFood);


//Check Age to Vote
function checkAge (age , callback){
  if(age >= 18){
    callback(`You can vote.`);
  }
  else{
    callback(`You cannot vote.`);
  }
}

checkAge(15 , (message) => {
 console.log(message);
});
