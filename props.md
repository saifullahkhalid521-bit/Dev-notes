# Week 9: React Props - Quick Notes

## 1. Props Kya Hain?
Props (Properties) matlab **component ke parameters**. 
Jaise JavaScript function mein hum arguments pass karte hain, waise hi React component mein data pass karne ke liye Props ka use hota hai. Parent component Child component ko Props ke through data bhejta hai. 

**Rule:** Props **read-only** hote hain. Child component inhe change nahi kar sakta.

## 2. Basic Props (String & Number)
JSX mein props ko HTML attributes ki tarah likhte hain. String ke liye `"..."` aur baaki cheezon (number, boolean, variable) ke liye `{}` use karte hain.

**Child Component:**
```jsx
// Destructuring use karna best practice hai
export function Greeting({ name, age }) {
  return <h2>Hello {name}, you are {age} years old.</h2>;
}
Parent Component:
<Greeting name="Saifullah" age={22} /> 
// Dhyan do: age ek number hai isliye {} mein hai
```
