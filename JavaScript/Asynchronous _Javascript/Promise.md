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
new Promise((resolve, reject) => {
  const isSuccess = true;

  if (isSuccess) {
    resolve("Data successfully received");
  } else {
    reject("Something went wrong");
  }
}).then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });