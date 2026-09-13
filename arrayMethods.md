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
1. 10 → true  → keep
2. 15 → false → remove
3. 20 → true  → keep
4. 25 → false → remove
5. 30 → true  → keep


* Difference btween map and filter
1. map()     → har element ko transform karta hai
2. filter()  → elements ko condition ke basis par select karta hai