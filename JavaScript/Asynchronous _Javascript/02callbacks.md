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
## Callback Hell
* Callback hell ek situation hai jaha multiple nested callbacks ka use hota hai, jisse code ko samajhna aur maintain karna mushkil ho jata hai. 

*Jab ek async kaam complete hone ke baad doosra async kaam start karna ho, hum uska callback pehle callback ke andar likhte hain.

* Callback hell ko avoid karne ke liye promises ya async/await ka use kiya jata hai.

### Example of Callback Hell

1. User fetch karo  
2. Us user ke orders fetch karo  
3. First order ki payment fetch karo

```javascript
function getUser(callback) {
  setTimeout(() => {
    console.log("User mil gaya");
    callback({ id: 1, name: "Saif" });
  }, 1000);
}

function getOrders(userId, callback) {
  setTimeout(() => {
    console.log("Orders mil gaye");
    callback([
      { id: 101, product: "Laptop" },
      { id: 102, product: "Mouse" }
    ]);
  }, 1000);
}

function getPayment(orderId, callback) {
  setTimeout(() => {
    console.log("Payment mil gayi");
    callback({ orderId, status: "Paid" });
  }, 1000);
}

// In functions ko sequence mein chalane ka callback way:

getUser((user) => {
  getOrders(user.id, (orders) => {
    getPayment(orders[0].id, (payment) => {
      console.log("Final payment:", payment);
    });
  });
});
```
##### Flow of execution:
getUser
  └─ getOrders
       └─ getPayment
            └─ final result

Output:
User mil gaya
Orders mil gaye
Payment mil gayi
Final payment: { orderId: 101, status: 'Paid' }


## callbacks hell error handling

* Callback hell with error handling tab hota hai jab multiple async tasks ko sequence mein run karte waqt callbacks ek ke andar ek nest hote jaate hain, aur har level par error check karna padta hai.

* Isse code right side mein failta hai, repeat hota hai, aur read/maintain karna difficult ho jata hai.

### Example
```javascript
function getUser(callback) {
  setTimeout(() => {
    callback(null, { id: 1, name: "Saif" });
  }, 1000);
}

function getOrders(userId, callback) {
  setTimeout(() => {
    if (userId !== 1) {
      callback("Orders not found", null);
      return;
    }

    callback(null, [{ id: 101, product: "Laptop" }]);
  }, 1000);
}

function getPayment(orderId, callback) {
  setTimeout(() => {
    if (orderId !== 101) {
      callback("Payment not found", null);
      return;
    }

    callback(null, { orderId, status: "Paid" });
  }, 1000);

  //Ab inko sequence mein, error handling ke saath call karo:

  getUser((userError, user) => {
  if (userError) {
    console.log("User error:", userError);
    return;
  }

  getOrders(user.id, (ordersError, orders) => {
    if (ordersError) {
      console.log("Orders error:", ordersError);
      return;
    }

    getPayment(orders[0].id, (paymentError, payment) => {
      if (paymentError) {
        console.log("Payment error:", paymentError);
        return;
      }

      console.log("Final payment:", payment);
    });
  });
});

/* Output:
Final payment: { orderId: 101, status: 'Paid' }
*/
}
```

* Har callback ke andar next async function aur uska error check likha hua hai. Isi nested/repeated structure ko callback hell with error handling bolte hain.