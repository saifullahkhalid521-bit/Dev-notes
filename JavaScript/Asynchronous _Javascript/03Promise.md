# Promise

* A Promise is an object representing the eventual completion or failure of an asynchronous operation.

### Tree States of a Promise
1. **Pending**: Initial state, neither fulfilled nor rejected.
2. **Fulfilled**: The operation completed successfully.
3. **Rejected**: The operation failed.

### Example of a Promise:

```javascript
const promise = new Promise((resolve, reject) => {
  const isSuccess = true;

  if (isSuccess) {
    resolve("Data successfully received");
  } else {
    reject("Something went wrong");
  }
});

//to consume the result of the promise

promise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });

  /* Output:
  Data successfully received
  if isSuccess is false, then output will be:
  Something went wrong
  */
 ```
 * We can also write promises without using variable like this:

 ```javascript  
new Promise((resolve, reject) => {});
```

* we can also use multiple `.then()` methods to handle the result of a promise:
* the nested `then()` will take the return value of the previous `then()` as its input as shown in the example below:

```javascript
const promiseFour = new Promise ((resolve , reject)=>{
  setTimeout(()=>{
    let error = false;
    if(!error){
      resolve({username: "Robot" , password: 1234});
    }
    else{
      reject("ERROR: something went wrong.");
    }
  },1000)
})

promiseFour
.then((data)=>{
  console.log(data);
  // console.log(data.username);
  return data.username;
})
.then((username)=>{
  console.log(username);
})
.catch((message)=>{
  console.log(message);
}).finally(()=> console.log(`Promise is either resolved or rejected.`));
```
##### Finally()
* ye hamesa chalega chahe promise resolve ho ya reject ho.


## Promise consomption using async/await

#### Example of async/await:
```javascript
const promiseFive = new Promise ((resolve , reject)=>{
  setTimeout(()=>{
    let error = true;
    if(!error){
      resolve({username: "JavaScript" , password: 123 })
    }
    else{
      reject("ERROR: JS went wrong!");
    }
  }, 1000)
})

async function consumePromiseFive(){
  try{
     const response = await promiseFive
  console.log(response);
  } catch (error) {
    console.log(error);
  } finally{
    console.log(`Promise is either resolved or rejected.`);
  }
}

consumePromiseFive();
```

1. async kya karta hai?

*Jis function ke aage async lagate ho, woh function automatically ek Promise return karta hai.

```javascript
async function test() {
  return "Hello";
}

test().then((data) => console.log(data));

//Andar se tumne string return ki, but async ne usse internally Promise ke successful result mein wrap kar diya.


async function name() {
  // await yahan use kar sakte ho
}

// await normally sirf async function ke andar likha ja sakta hai.
```
2. await kya karta hai?
* await kisi Promise ka final result aane ka wait karta hai.

```javascript
const response = await promiseFive;
/*iska matlba:
“promiseFive complete hone do. Agar success hua to resolved value response mein store karo; agar fail hua to error throw karo.”

Yeh await wala code callback nesting ke bina sequential, normal code jaisa dikhta hai.
```
* promiseFive abhi pending hai, isliye consumePromiseFive function ka execution us line par temporarily ruk jata hai.
*Lekin important point:
1. Pura JavaScript ya browser rukta nahi hai—sirf consumePromiseFive function wait karta hai.

2. Baaki code/chizein chal sakti hain.

```javascript
let error = true;
if (!error)
//!true means false, so if block nahi chalega. else chalega:
reject("ERROR: JS went wrong!");
//Pending → Rejected
```

* await rejection ko error ki tarah treat karta hai
1. Agar promise reject hota hai, ye line:
```javascript
const response = await promiseFive;
// normal value return nahi karti. Iski jagah rejection value ko error ki tarah throw kar deti hai.
```
Isliye console.log(response) nahi chalega.

#### catch 
* catch error handle karta hai
```javascript
catch (error) {
  console.log(error);
}
//output: ERROR: JS went wrong!
//catch mein error naam bas variable ka naam hai. Tum message ya err bhi use kar sakte ho:
catch (message) {
  console.log(message);
}

//Agar error = false kar do
let error = false;
//then
resolve({ username: "JavaScript", password: 123 });
/*Promise state: Pending → Fulfilled
Ab await resolved object ko response mein dega:*/
const response = await promiseFive;
//Output: 
{ username: 'JavaScript', password: 123 }
```
* we can use .then().catch() or async/await for promise consumption. Both are valid ways to handle promises in JavaScript. 

#### One-line meaning of async/await:
1. async = function ko Promise-based banata hai
2. await = Promise ka result aane ka wait karta hai
3. try = success code
4. catch = rejected/error code
5. finally = har case mein run hota hai

## Promise chaining

* Promise Chaining in JavaScript means running multiple asynchronous tasks one after another, where the result of one Promise is passed to the next .then().

#### Example of Promise chaining:
```javascript
function placeOrder() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Order placed!");
    }, 1000);
  });
}

function makePayment(message) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(message + " Payment successful!");
    }, 1000);
  });
}

function prepareFood(message) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(message + " Food prepared!");
    }, 1000);
  });
}

function deliverFood(message) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(message + " Food delivered!");
    }, 1000);
  });
}


// Promise Chaining
placeOrder()

  // Order complete → Payment start
  .then((result) => {
    console.log(result);
    return makePayment(result);
  })

  // Payment complete → Food preparation start
  .then((result) => {
    console.log(result);
    return prepareFood(result);
  })

  // Food ready → Delivery start
  .then((result) => {
    console.log(result);
    return deliverFood(result);
  })

  // Delivery complete
  .then((result) => {
    console.log(result);
  })

  // Agar koi error aaye
  .catch((error) => {
    console.log("Error:", error);
  });
```
#### Using fetch API with Promise chaining:
```javascript
// Pehle users ka data fetch hoga
fetch("https://jsonplaceholder.typicode.com/users/1")

  // Response ko JSON mein convert karo
  .then((response) => {
    return response.json();
  })

  // JSON data milne ke baad user ka name nikalo
  .then((user) => {
    console.log("User:", user.name);

    // Ab next API call kar sakte hain
    return fetch(
      `https://jsonplaceholder.typicode.com/posts?userId=${user.id}`
    );
  })

  // Posts ka response JSON mein convert karo
  .then((response) => {
    return response.json();
  })

  // Finally posts mil jayenge
  .then((posts) => {
    console.log("Posts:", posts);
  })

  // Kisi bhi step mein error aaye
  .catch((error) => {
    console.log("Error:", error);
  });
  ```
  ## Promise.all()
* Promise.all() is a method that takes an array of promises and returns a single promise that resolves when all of the promises in the array have resolved, or rejects if any of the promises reject. 
* It returns an array of results in the same order as the promises were passed in, regardless of the order in which they resolve.

#### Example of Promise.all():
```javascript
async function getData() {
    try {
        const [users, posts] = await Promise.all([
            //here we are useig destructuring assignment to assign the resolved values of the promises to the variables users and posts.
            // Users API
            fetch("https://jsonplaceholder.typicode.com/users")
                .then(res => res.json()),

            // Posts API
            fetch("https://jsonplaceholder.typicode.com/posts")
                .then(res => res.json())
        ]);

        console.log("Users:", users);
        console.log("Posts:", posts);

    } catch (error) {
        console.log("Error:", error.message);
    }
}
getData();
//this aproch will be useed in react js to fetch multiple data at a time and then use it in the component.
```

#### more easy example of Promise.all():
```javascript
// 3 promises banao

const chai = new Promise((resolve) => {
    setTimeout(() => resolve('☕ Chai ready'), 5000);
});

const paratha = new Promise((resolve) => {
    setTimeout(() => resolve('🫓 Paratha ready'), 10000);
});

const anda = new Promise((resolve) => {
    setTimeout(() => resolve('🥚 Anda ready'), 7000);
});

// Ab teeno ek saath start karo
console.log('Kaam shuru...');

Promise.all([chai, paratha, anda])
    .then((results) => {
        console.log('Sab ready:', results);
        // Output after 10 seconds:
        // Sab ready: ['☕ Chai ready', '🫓 Paratha ready', '🥚 Anda ready']
    })
    .catch((error) => {
        console.log('Kuch galat:', error);
    });
```
* Dhyan do: Total time 10 second laga, na ki 5+10+7 = 22 second. Kyunki teeno ek saath start hue.

#### simple example with fetch
```javascript
// 3 different users ka data ek saath lao

const user1 = fetch('https://api.github.com/users/octocat')
    .then(response => response.json());

const user2 = fetch('https://api.github.com/users/gaearon')
    .then(response => response.json());

const user3 = fetch('https://api.github.com/users/sindresorhus')
    .then(response => response.json());

Promise.all([user1, user2, user3])
    .then((users) => {
        // users ek array hai
        console.log(users[0].name);  // The Octocat
        console.log(users[1].name);  // Dan Abramov
        console.log(users[2].name);  // Sindre Sorhus
    })
    .catch((error) => {
        console.log('Koi ek user fail hua:', error);
    });
```

### Error handling in Promise.all()
```javascript
const p1 = new Promise((resolve) => {
    setTimeout(() => resolve('Success 1'), 1000);
});

const p2 = new Promise((resolve, reject) => {
    setTimeout(() => reject('❌ P2 fail ho gaya'), 2000);
});

const p3 = new Promise((resolve) => {
    setTimeout(() => resolve('Success 3'), 3000);
});

Promise.all([p1, p2, p3])
    .then((results) => {
        // ❌ Yeh kabhi nahi chalega
        console.log('Sab success:', results);
    })
    .catch((error) => {
        // ✅ Yeh chalega
        console.log('Error:', error);  // "❌ P2 fail ho gaya"
    });
```
* Matlab: p1 aur p3 success the, lekin p2 fail hone ki wajah se poora result discard ho gaya.

## Promise.race
* Promise.race() multiple Promises ko start karta hai, lekin jo Promise sabse pehle resolve hota hai, uska result le leta hai

```javascript
const p1 = new Promise(resolve => {
    setTimeout(() => resolve("Promise 1"), 2000);
});

const p2 = new Promise(resolve => {
    setTimeout(() => resolve("Promise 2"), 1000);
});

const result = await Promise.race([p1, p2]);

console.log(result);
// Output: "Promise 2" (kyunki p2 pehle resolve hua)
```

#### Real-world example of Promise.race():
* Maan le tu kisi API ko call kar raha hai, but tu chahta hai:
* "Agar API 3 seconds ke andar response nahi deti, toh timeout/error de do."
```javascript
const api = fetch("https://jsonplaceholder.typicode.com/users");

const timeout = new Promise((_, reject) => {
    setTimeout(() => {
        reject(new Error("Request timed out"));
    }, 3000);
});

try {
    const response = await Promise.race([api, timeout]);

    console.log("Response received:", response);

} catch (error) {
    console.log("Error:", error.message);
}
/* Agar API 3 seconds ke andar response nahi deti, toh "Request timed out" error milega.
Agar API 3 seconds ke andar response deti hai, toh woh response milega.
*/
```