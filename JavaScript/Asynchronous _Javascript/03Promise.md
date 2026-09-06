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