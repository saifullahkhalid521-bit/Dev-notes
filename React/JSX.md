# JSX

JSX is a syntax extension for JavaScript that allows you to write HTML-like code in your JavaScript files. It is used with React to define what the UI should look like.

Naam thoda technical lagta hai, but concept bahut simple hai.

JSX allows us to write HTML-like syntax inside JavaScript.

Vanilla JavaScript mein:

```javascript
const username = "Saifullah";

const heading = document.createElement("h1");
heading.textContent = `Hello ${username}`;


React JSX mein:
const username = "Saifullah";

const heading = <h1>Hello {username}</h1>;
```


* Dekha? React mein HTML jaisa syntax directly JavaScript file ke andar likh sakte hain.

Yahi JSX hai.
4. Understanding JSX syntax
Let's break this code into small pieces.

```javascript
const username = "Saifullah";

const heading = <h1>Hello {username}</h1>;


Part 1:
const username = "Saifullah";


Normal JavaScript variable hai. Ismein username store hai.

Part 2:
<h1>Hello {username}</h1>


Yahan:
- <h1> = HTML-like heading element.
- Hello = Normal text.
- {username} = JavaScript expression.
Why do we use curly braces {}?
JSX mein jab bhi humein JavaScript variable ya expression use karna hota hai, hum curly braces {} lagate hain.

Example:
const age = 22;

const user = <p>My age is {age}</p>;


Another example:
const a = 10;
const b = 20;

const result = <h2>Total: {a + b}</h2>;

```

Output:
Total: 30
What the JSX expression displays in the browser.

* Remember: {} JSX ke andar JavaScript expressions likhne ke liye hain. Normal JavaScript statements jaise if aur for directly JSX ke andar nahi likhte.

5. Important JSX rules
There are a few rules you must understand before writing bigger components.

```javascript
Rule 1: Return one parent element
Incorrect
function App() {
  return (
    <h1>Hello</h1>
    <p>Welcome</p>
  );
}


Why incorrect? React components should return one parent element.
Correct
function App() {
  return (
    <div>
      <h1>Hello</h1>
      <p>Welcome</p>
    </div>
  );
}


You can also use a Fragment:
function App() {
  return (
    <>
      <h1>Hello</h1>
      <p>Welcome</p>
    </>
  );
}


<> </> is a Fragment. It groups elements without adding an extra HTML element to the page.

Rule 2: Use className instead of class

HTML:
<div class="card"></div>


JSX:
<div className="card"></div>


Why? React uses className as the JSX attribute for HTML classes.

Rule 3: Close every tag

HTML:
<img src="photo.jpg">


JSX:
<img src="photo.jpg" />


Rule 4: JavaScript expressions go inside {}
const name = "Saifullah";
const isStudent = true;

function App() {
  return (
    <div>
      <h1>{name}</h1>
      <p>{isStudent ? "Student" : "Not a student"}</p>
    </div>
  );
}
```