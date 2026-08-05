# Closures

A closure is a function that or return gives the reference to this parantes scope, and keep alive the variables of the parent scope unlike regular functions.

## Example
```javascript

const add = (a) => {
  return (b) => {
    return a + b;
  }
}

const add5 = add(5);
console.log(add5(3)); // Output: 8

function greet (name){
  return function greetings (){
    return `Hello, ${name}`;
  }
}
const greetSaif = greet("Saif");
console.log(greetSaif()); // Output: Hello, Saif
``` 
in the above examples , inner functions are useing the lexical scope of the outer function.

## Example 
### Bank Account
```javascript
    const createBankAccount = (n) => {

      let currentBalance = n;
    const accountData = {
      "deposit" : function (a) {
        currentBalance+=a;
        console.log("Balance: " + currentBalance); 
      },
      "withdraw" : function (b) {
        currentBalance-=b;
        console.log("Balance: " + currentBalance);
      },
      "balance" : function () {
        console.log("Balance "+currentBalance);
      }
    }
  return accountData;
}

const account = createBankAccount(1000);

account.deposit(500);

account.withdraw(200);

account.balance();
```
