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
```
## 5. Passing Functions as Props
Event handling ke liye hum functions ko props ki tarah pass karte hain.

Rule (Important): Function ko pass karte waqt () mat lagao. Sirf function ka naam (reference) do, warna wo turant run ho jayega.

```jsx
Child Component:

export function AlertButton({ onClickAction, label }) {
  return <button onClick={onClickAction}>{label}</button>;
}

Parent Component:

function handleClick() {
  console.log("Button clicked!");
}

<AlertButton label="Click Me" onClickAction={handleClick} />
// onClickAction={handleClick} sahi hai, handleClick() nahi.
```
## 6. Common Mistakes to Avoid
Props ko change mat karo (e.g., props.name = "new" mat likho).

Number pass karte waqt age="22" nahi, age={22} likho (warna wo string ban jayega).

Object pass karte waqt data={ {title: "..."} } aise likho, data="{title: '...'}" nahi.

text

---

Ye notes bilkul crisp hain. Tum bina jaldi kiye inko ek baar padh lena, aur aaj ka code ek baar dekh lena. Jab next topic (List Rendering) ke liye ready ho, tab mujhe batao!