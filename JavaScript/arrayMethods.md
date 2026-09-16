# Topics
1. map() method
2. filter() method
3. find() method
4. some() method
5. every() method
6. reduce() method
7. sort() method

________________________________________________________________________________________________________________________________________

# Map() method
* It accepts a callback and applies that function to each element of an array, then return a new array.

#### Comman Syntax
```javaScript
const number = [1 ,2 , 3 ,4 ,5];
const double = number.map((elem)=>{
  return elem * 2;
});
console.log(double);
//OR

const Double = number.map(square);
function square (elem) {
  return elem * 2;
}
console.log(Double);
```

* in map method we have three arguments in the callback , element ,Index and array. we can use these properties to get the index element and complete array.

### Exapmle 
```javaScript

const names = ["Saif", "Robot", "Ego"];

const result = names.map((elem, index, array) => {
    return `${index}: ${elem}: ${array}`;
});

console.log(result);

```

* Using split with map()
```javaScript
const dates = ["2024-1-10" , "2025-2-20" , "2026-3-30"];
const formattedDates = dates.map(formatDates);

console.log(formattedDates);

function formatDates(element){
  const parts = element.split("-");
  return `${parts[1]}/${parts[2]}/${parts[0]}`;
}
```

## map() ka return behavior 
* map() callback ke return value ko new array ke element ke roop mein store karta hai.

```javaScript
const numbers = [1, 2, 3];

const result = numbers.map((elem) => {
    return elem * 2;
});

console.log(result);
/*output
[2 , 4 , 6]
*/

// Agar return nahi kiya?

const numbers = [1, 2, 3];
const result = numbers.map((elem) => {
    elem * 2;
});
console.log(result);
/* [undefined, undefined, undefined]
Why?
Because { } wale arrow function mein explicit return chahiye.*/
```
__________________________________________________________________________________________________________________________________


# filter() method
* Array ke andar se condition satisfy karne wale elements ko select karke ek NEW array return karna.

```javaScript
const numbers = [10, 15, 20, 25, 30];

const evenNumbers = numbers.filter((elem) => {
    return elem % 2 === 0;
});

console.log(evenNumbers);
/*Output
[10, 20, 30]*/
```
* filter() ka callback true/false decide karta hai:
1.  10 → true  → keep
2.  15 → false → remove
3.  20 → true  → keep
4.  25 → false → remove
5.  30 → true  → keep
 

* Difference btween map and filter
1. map()     → har element ko transform karta hai
2. filter()  → elements ko condition ke basis par select karta hai

* Using map with filter
```javaScript
const orders = [
  { id: 1, total: 120, status: "shipped" },
  { id: 2, total: 80, status: "pending" },
  { id: 3, total: 200, status: "shipped" },
  { id: 4, total: 50, status: "shipped" }
];
// Get IDs of shipped orders over $100 → [1, 3]

const fitlerOrders = orders.filter((elem)=>{
  return elem.total > 100 && elem.status === 'shipped';
}).map((elem)=>{
  return elem.id;
})
console.log(fitlerOrders);
```

#### Advansed usage of filter
```javaScript
const nums = [1 , 2 ,2 , 3 , 4 , 4 ,5 ,1 ];
const filterNums = nums.filter((elem , i)=>{
  return nums.indexOf(elem) === i;
})
console.log(filterNums);
```

* Build reusable filters
```javaScript
const isEven = n => n % 2 === 0;
const isPositive = n => n > 0;
const isMultipleOf = (n, m) => n % m === 0;

// Then apply: positive even numbers divisible by 3
const numsF = [9 , -2 , 4 , 12 , 18 , 24];
const result = numsF
  .filter(isPositive)
  .filter(isEven)
  .filter(n => isMultipleOf(n, 3));
console.log(result);
```

* in filter's argument we also have element , index and array same as map () method and we can use then to get expected results.
```JavaScript
const numbers = [10, 20, 10, 30, 20];

// Remove duplicate numbers
const uniqueNumbers = numbers.filter((element, index, array) => {
  return array.indexOf(element) === index;
  //Logic: array.indexOf(10) returns 0 (the first place 10 appears). At position 2, 0 === 2 is false, so the duplicate 10 is filtered out.
});
console.log(uniqueNumbers); // Output: [10, 20, 30]
```

_________________________________________________________________________________________________________________________________________


# find() method
* find() returns the FIRST element that matches a condition. If nothing matches, it returns undefined.

* filter() gives you all matches (in an array). find() gives you the first match (a single value).

* Here also we have element , index and array but index and array are used very rarely

```JavaScript
const nums = [1, 3, 5, 6, 7, 8];
const firstEven = nums.find(n => n % 2 === 0);
console.log(firstEven); 

/* Output = 6
Only 6 is returned (not 8), because find stops at the first match.*/

const nums = [1, 3, 5];
const result = nums.find(n => n % 2 === 0);
console.log(result); // undefined


const dupli = [1 , 2 , 3 , 4 , 2 , 5];
const findDupli = dupli.find((elem , i) => dupli.indexOf(elem) !== i);
console.log(findDupli);
/*Output -> 2*/
```
#### Rule of Thumb.
* Need one specific item (by id, name, etc.)? → find()
*Need a list of all matches? → filter()

________________________________________________________________________________________________________________________________________


# some() method
* some() returns true if AT LEAST ONE element passes the test, otherwise false , have elem , index and array.

* Return value: Always a boolean (true or false) — never an array, never an element.

### simple example
```JavaScript
const nums = [1, 3, 5, 6, 7];
const hasEven = nums.some(n => n % 2 === 0);
console.log(hasEven); // true (6 is even)
```
#### Difference btw some() & find()
```JavaScript
const nums = [1, 2, 3, 4];

nums.find(n => n > 3); // 4      ← element
nums.some(n => n > 3); // true   ← boolean
```

* it's mostly used for validation like 
```JavaScript
const fields = ["john", "", "doe"];
const hasEmpty = fields.some(f => f.trim() === "");
console.log(hasEmpty); // true

const nums = [1, 2, 3, 4];
nums.some(n => {
  console.log("checking", n);
  return n === 2;
});
/*checking 1
checking 2
It stops after finding 2 — never checks 3 or 4. This is short-circuiting in action.*/
```

_________________________________________________________________________________________________________________________________________

# every() method
* every() returns true if ALL elements pass the test, otherwise false. it also have element , index and array

* Return value: Always a boolean — never an array, never an element. 

### Example
```JavaScript
const nums = [1, 2, 3, 4, 5];
console.log(nums.every(n => n > 0)); // true

// Are all strings non-empty?
const words = ["apple", "banana", "cherry"];
console.log(words.every(w => w.length > 0)); // true

const words2 = ["apple", "", "cherry"];
console.log(words2.every(w => w.length > 0)); // false
```

#### Empty array --> always true with .every()
```JavaScript
[].every(() => false); // true (!)
//Why? Logically, "all elements satisfy X" is trivially true when there are no elements. (Same reason every in math is true for empty sets.)
```

______________________________________________________________________________________________________________________________________

# reduce() method

* reduce() poore array ko process karke usse ek single final value mein convert karta hai.

* The callback must return something — whatever it returns becomes the new accumulator for the next iteration.

* reduce() is the most flexible — you can technically implement map, filter, find using just reduce. But don't — use the right tool for the job.

### Rule:
1. Always pass an initial value unless you have a very specific reason not to.

2. (accumulator, currentValue) — accumulator first, current second. Mixing them up is the #1 beginner bug.

3. Callback MUST return something.

#### Simple example and syntax
```JavaScript
//syntax
array.reduce((accumulator, currentValue, index, array) => {
  // return the new accumulator
}, initialValue);

//example
const numbers = [10, 20, 30, 40];
const total = numbers.reduce((acc, elem) => {
  return acc + elem;
}, 0);

console.log(total);
//OutPut -> 100
```


#### Imp example of Object with reduce for count.
```JavaScript
const fruits = ["apple","banana","apple","cherry","banana","apple"];
// Yahan final value ek OBJECT {} hogi.
//
// acc   = accumulator → hamara result object
// fruit = current element → current fruit
//
// {} = initial value of accumulator
const count = fruits.reduce((acc, fruit) => {

  // acc[fruit] ka matlab:
  //
  // Agar fruit = "apple"
  // toh acc[fruit] = acc["apple"]

  // Pehli baar apple aayega toh:
  // acc["apple"] → undefined

  // undefined || 0 → 0
  // 0 + 1 → 1
  // So:
  // acc["apple"] = 1

  // Agar apple pehle se exist karta hai:
  //
  // acc["apple"] → 1

  // 1 || 0 → 1
  // 1 + 1 → 2
  // So:
  // acc["apple"] = 2

  acc[fruit] = (acc[fruit] || 0) + 1;

  // Updated accumulator ko return karna zaroori hai.
  // Ye returned object next iteration ka accumulator banega.
  return acc;

}, {}); // reduce() ka accumulator initially empty object hai


console.log(count);

// Output: {   apple: 3,   banana: 2,  cherry: 1 }

/*if (acc[fruit] > 0) {
  acc[fruit] = acc[fruit] + 1;
} else {
  acc[fruit] = 1;
}*/
//same logic
```


#### Imp example of Object with reduce for group.
```JavaScript
const users = [
  { name: "Alice", role: "admin" },
  { name: "Bob", role: "user" },
  { name: "Charlie", role: "admin" },
  { name: "Dave", role: "user" }
];

const grouped = users.reduce((acc, user) => {

  // Agar is role ka group abhi exist nahi karta,
  // toh us role ke naam se ek empty array create karo.
  if (!acc[user.role]) {
    acc[user.role] = [];
  }

  // Current user ko uske role wale array mein add karo.
  acc[user.role].push(user);

  // Updated accumulator ko next iteration ke liye return karo.
  return acc;

}, {});

console.log(grouped);
```

_________________________________________________________________________________________________________________________________________


# sort() method
* sort() rearranges the elements of an array based on a comparison rule you provide.

## Sort Traps
### 1st trap
* Every method you've learned so far (map, filter, find, some, every, reduce) returns a new array or value. sort() does NOT.
```JavaScript
const nums = [3, 1, 2];
const sorted = nums.sort();

console.log(sorted); // [1, 2, 3]
console.log(nums);   // [1, 2, 3] ← ORIGINAL CHANGED!

//Safe pattern: copy first
const nums = [3, 1, 2];
const sorted = [...nums].sort();   // spread creates a copy
console.log(nums);   // [3, 1, 2]   ← untouched
console.log(sorted); // [1, 2, 3]
```
### 2nd trap
* Without a comparison function, sort() converts everything to strings and compares them lexicographically (dictionary order).

```JavaScript
const nums = [10, 1, 5, 100, 25];
nums.sort();
console.log(nums); // [1, 10, 100, 25, 5]  ← 😱 NOT numerically sorted!

//Why? Because "10" < "5" alphabetically (since "1" < "5" as characters).
// This is the #1 gotcha with sort().
```
### The Comparison Function -- How it Works
* To sort properly, you pass a comparator: (a, b) => ...

* The comparator returns:

* Negative number → a comes before b

* Zero → keep order (a and b are "equal")

* Positive number → a comes after b

1. Return < 0  →  [a, b]   (a first)
2. Return 0    →  [a, b]   (order preserved)
3. Return > 0  →  [b, a]   (b first)

* Ascending
(a, b) => a - b

* Descending
(a, b) => b - a
```JavaScript
// Sort numbers ascending and descending
const nums = [10, 1, 5, 100, 25];

// Ascending
const asc = [...nums].sort((a, b) => a - b);
console.log(asc); // [1, 5, 10, 25, 100]

// Descending
const desc = [...nums].sort((a, b) => b - a);
console.log(desc); // [100, 25, 10, 5, 1]
```

### Imp
* by defalt sort we arange the array according to alphabeticaly by therefor strings with capital letters will come first then small letters as shown in the example

#### Example
```JavaScript
const words = ["Banana", "apple", "Cherry"];
words.sort();
console.log(words); // ["Banana", "Cherry", "apple"]  ← uppercase first!

// to fix it we have to use localCompare()

//localeCompare() is the "correct" way to compare strings (handles accents, case, etc.).
words.sort((a, b) => a.toLowerCase().localeCompare(b.toLowerCase()));

// side code 
"apple".localeCompare("banana"); // -1
"banana".localeCompare("apple"); // 1
"apple".localeCompare("apple");  // 0
```

## ⚠️ Gotchas to Remember

1. Mutates the original array
```javascript
const a = [3, 1, 2];
a.sort();
console.log(a); // [1, 2, 3] — original changed
```

2. Default sort is alphabetical (string comparison)
```javascript
[10, 9, 8].sort(); // [10, 8, 9]  ← wrong!
[10, 9, 8].sort((a, b) => a - b); // [8, 9, 10]  ← correct
```

3. Comparator must return a number
```javascript
nums.sort((a, b) => a > b);  // ❌ returns boolean (true/false)
nums.sort((a, b) => a - b);  // ✅ returns number
```
* true coerces to 1, false to 0. So a > b gives 0 when a < b — which means "keep order" instead of "swap". Silent bug!


4. Not stable in ancient browsers (but is in modern JS)
* Modern JS guarantees sort() is stable — items that compare equal keep their original order. So you don't need to worry anymore.


5. localeCompare vs < for strings
```javascript
"apple" < "banana";                    // true (works)
"apple".localeCompare("banana");       // -1 (better — handles accents, case)
```
* For real apps, prefer localeCompare.


6. Comparator with undefined fields can crash
```javascript
[{a: 1}, {}].sort((x, y) => x.a - y.a); // NaN comparisons — undefined behavior
```
* Always guard with ?? 0 if fields may be missing.

```JavaScript
```
