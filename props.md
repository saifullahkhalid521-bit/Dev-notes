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
## 3. Default Props (Backup Values)
Agar parent ne koi prop pass nahi kiya, toh error na aaye isliye hum function parameters mein default value set kar dete hain.

```jsx
export function Button({ text, color = "blue" }) {
  // Agar color prop nahi milega, toh "blue" use hoga
  return <button style={{ backgroundColor: color }}>{text}</button>;
}
Parent:

<Button text="Submit" />           {/* Output: Blue button */}
<Button text="Delete" color="red" /> {/* Output: Red button */}
```
## 4. Passing Objects as Props
Hum direct object bhi prop ke roop mein bhej sakte hain. Object bhejte waqt double curly braces {{ }} lagte hain (ek React ke liye, ek JS object ke liye).

```jsx
Child Component:

export function Product({ data }) {
  return (
    <div>
      <h3>{data.title}</h3>
      <p>Price: ₹{data.price}</p>
      <p>Tags: {data.tags.join(" | ")}</p>
    </div>
  );
}

Parent Component:

<Product data={{ title: "Laptop", price: 50000, tags: ["tech", "electronics"] }} />
