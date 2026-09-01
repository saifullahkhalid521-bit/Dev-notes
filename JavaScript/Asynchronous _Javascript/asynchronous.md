# Asynchoronous JavaScript

* 1 JavaScript ek time par ek hi line execute karti hai
JavaScript ka main code line-by-line chalta hai. Lekin slow tasks—timer, API request, file/database work—ko browser/Node handle karne ke liye bhej deta hai.

* 2 setTimeout code ko block nahi karta
Ye galat sochna hai , “JavaScript timer register karti hai aur turant aage ke code par chali jaati hai.”

* 3 Timer ka delay minimum waiting time hota hai
Agar tum 2000 likhte ho, iska matlab “kam se kam 2 seconds baad run karna.” Exactly 2 seconds par hi run hoga, ye guaranteed nahi—agar JavaScript busy hui toh thoda late chal sakta hai.

* 4 Timer ke andar wali function later run hoti hai

```javascript
setTimeout(() => {
  console.log("This runs later");
}, 2000);
console.log("This runs first");
```
*(() => { ... }) ek function hai jo abhi run nahi ho raha. JavaScript ise save kar leti hai aur time complete hone par run karti hai.


## Topics

* Callbacks
* Promises
* Async/Await