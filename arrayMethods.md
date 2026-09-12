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

* Using split and map()
```javaScript
const dates = ["2024-1-10" , "2025-2-20" , "2026-3-30"];
const formattedDates = dates.map(formatDates);

console.log(formattedDates);

function formatDates(element){
  const parts = element.split("-");
  return `${parts[1]}/${parts[2]}/${parts[0]}`;
}
```