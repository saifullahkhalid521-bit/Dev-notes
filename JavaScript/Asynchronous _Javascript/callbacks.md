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
```


## Error Handling in Callbacks

```javascript
function getUser(callback) {
  console.log("User fetch ho raha hai...");

  setTimeout(() => {
    const user = {
      id: 1,
      name: "Saif"
    };

    callback(user);
  }, 2000);
}

getUser((userData) => {
  console.log("User mil gaya:", userData);
});
```
* uper wale example mai id 1 use ho raha hai but what if user id 2 ye koi or id dale , in that case we can handle error in callback function by passing an error as the first argument.

```javascript
function getUser(id, callback) {
  console.log("User fetch ho raha hai...");

  setTimeout(() => {
    if (id === 1) {
      const user = {
        id: 1,
        name: "Saif"
      };

      callback(null, user);
    } else {
      callback("User not found", null);
    }
  }, 2000);
}

function callback(error, user) {
  if (error) {
    console.log("Error:", error);
    return;
    //yaha return is liye lagaya taki error aane k baad code aage execute he no ho. 
  }

  console.log("User mila:", user);
};

getUser(1, callback);
//Yahan id 1 hai, to success wala block chalega:
callback(null, user);
// Matlab callback receive karega:
error = null;
user = { id: 1, name: "Saif" };
/* Ourput:
User fetch ho raha hai...
User mila: { id: 1, name: 'Saif' }*/
// ----------------------------------------

// now in error case
getUser(5, callback);
//id === 1 false hai, to ye chalega:
callback("User not found", null);
//callback receive karega:
error = "User not found";
user = null;
/* Output:
User fetch ho raha hai...
Error: User not found*/
```
