# Topics
1. map() method
2. filter() method
3. find() method
4. some() method
5. every() method
6. reduce() method
7. sort() method


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