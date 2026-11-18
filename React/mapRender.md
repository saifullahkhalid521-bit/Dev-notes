# React Lists & `.map()` - Detailed Notes

## 1. `.map()` Kya Hai aur Kyun Use Karein?
React mein jab humare paas ek array of data hota hai (jaise 10 users ya 50 products), toh hum har item ke liye manually component ya HTML tag nahi likhte. Hum JavaScript ke `.map()` method ka use karte hain.
`.map()` ek array ko loop karta hai (jaise `for` loop) aur har item ko ek naye React Element (JSX) mein convert kar deta hai. Phir React un sabhi elements ko screen par render kar deta hai.

## 2. `.map()` ka Basic Syntax (JavaScript vs React)

**Normal JavaScript:**
```javascript
const numbers = [1, 2, 3];
const doubled = numbers.map((num) => {
  return num * 2;
});

React JSX ke andar:
JSX mein JavaScript chalane ke liye curly braces {} use hote hain.

``jsx
const fruits = ["Apple", "Banana", "Mango"];

function FruitList() {
  return (
    <ul>
      {fruits.map((fruit) => (
        <li>{fruit}</li>
      ))}
    </ul>
  );
}
```

