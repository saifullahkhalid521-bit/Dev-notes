```javaScript
const date = [
  "2026-10-15", // Future date
  "2026-11-01", // Future date
  "2024-03-20", // Past date 1
  "2026-12-25", // Future date
  "2025-08-05"  // Past date 2
];
const todayC = new Date(); 
const pastDataCheck = date.some(elem => new Date(elem) < todayC);
console.log(pastDataCheck);
```

# LocalStorage in JS
* localStorage browser ki chhoti storage hai jahan hum data save kar sakte hain, aur page/browser refresh ya close karne ke baad bhi data generally rehta hai.

```JavaScript
1. Kuch save karna

localStorage.setItem("name", "Saif");
Meaning:
"name" naam ke under "Saif" save kar do.


2. Data nikalna

localStorage.getItem("name");
Output:
"Saif"


3. Data delete karna

localStorage.removeItem("name");
Sab localStorage clear:
localStorage.clear();


⚠️ Sabse important point
localStorage sirf strings store karta hai.

Aur agar object/array store karna hai:
localStorage.setItem("user", JSON.stringify(user));

Wapas object chahiye:
const user = JSON.parse(localStorage.getItem("user"));
```

SAVE    → setItem()
GET     → getItem()
DELETE  → removeItem()
ALL     → clear()

Object → JSON.stringify()
String → JSON.parse()


### Example code
```javaScript
const user = {
  name: "Saif",
  age: 22,
  skills: ["JavaScript", "React", "Git"]
};

// Object → String → localStorage
localStorage.setItem("user", JSON.stringify(user));


// localStorage → String → Object
const savedUser = JSON.parse(localStorage.getItem("user"));

console.log(savedUser);
console.log(savedUser.name);
console.log(savedUser.skills);
```