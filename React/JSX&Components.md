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

6. JSX under the hood (Babel transpilation)
JSX is not valid JavaScript — the browser cannot understand it. Babel transpiles JSX into `React.createElement()` calls.

```javascript
// What you write
const heading = <h1>Hello {username}</h1>;

// What Babel produces
const heading = React.createElement("h1", null, "Hello ", username);
```

`React.createElement(type, props, ...children)` creates a React element (a plain object describing what to render). This is why every JSX file needs `React` in scope (or the automatic JSX runtime in modern setups).

7. Attributes and event handlers
- Attributes use camelCase, not kebab-case: `onClick`, `onChange`, `maxLength`, `backgroundColor`.
- HTML `for` → JSX `htmlFor`.
- Event handlers are props that accept a function:
  ```javascript
  function Button() {
    function handleClick() { alert("Clicked!"); }
    return <button onClick={handleClick}>Click me</button>;
  }
  ```
- Values are passed without quotes when they are expressions; use quotes for strings:
  ```javascript
  <img src={user.avatarUrl} alt="profile" />
  ```

8. Style attribute
Inline styles are an object with camelCase keys and string values (units required for numbers except unitless CSS properties):
```javascript
const divStyle = { color: "white", backgroundColor: "blue", borderRadius: "8px" };
<div style={divStyle}>Styled content</div>
```

9. Comments in JSX
Comments must be wrapped in curly braces and be valid JS expressions:
```javascript
<div>
  {/* This is a JSX comment */}
  <h1>Hello</h1>
</div>
```

10. Boolean, null, and undefined
- `false`, `null`, `undefined`, and `true` are ignored in JSX (nothing renders):
  ```javascript
  const show = false;
  const el = <div>{show}</div>; // renders nothing
  ```
- Boolean attributes are written without a value: `<input disabled />`.

11. Lists and the key prop
When rendering arrays, each item needs a unique `key` so React can track changes:
```javascript
const items = ["Apple", "Banana", "Cherry"];
<ul>
  {items.map((item) => (
    <li key={item}>{item}</li>
  ))}
</ul>
```
Use a stable unique identifier (e.g. an `id` from data) rather than the array `index` when items can be reordered or added/removed.

12. Conditional rendering
- Ternary operator: `<div>{isLoading ? <Spinner /> : <Content />}</div>`
- Logical `&&` (renders the element when true, nothing when false): `{hasMessages && <p>You have messages</p>}`
- Avoid `if`/`else` statements directly inside JSX — extract them to a helper function or render conditionally outside the JSX.

13. Fragment (named)
`<>` is shorthand for `<React.Fragment>`. Use the named form when you need to pass a `key`:
```javascript
<React.Fragment key="row">
  <td>Cell 1</td>
  <td>Cell 2</td>
</React.Fragment>
```

14. `dangerouslySetInnerHTML`
To render raw HTML, use the `dangerouslySetInnerHTML` prop with a `__html` key:
```javascript
<div dangerouslySetInnerHTML={{ __html: rawHtml }} />
```
Only use this when the content is trusted — it opens an XSS risk.

# Components

components are the building blocks of a React application. They allow you to split the UI into independent, reusable pieces that can be managed separately.

A component is simply a JavaScript function that returns JSX.

```javascript
For example:
function UserCard() {
  return (
    <div>
      <h2>Saifullah</h2>
      <p>Frontend Developer</p>
    </div>
  );
}
```

Let's break it down.
Syntax	Meaning
function	Creates a JavaScript function
UserCard	Component name
return	  Returns the UI
()	      Contains the JSX
<div>	    HTML-like element
</div>	  Closing element

Three important component rules:
1. Component names must start with a capital letter.
2. A component should return JSX (or null when nothing should be rendered).
3. Components can be reused multiple times.
For example:

```javaScript
function UserCard() {
  return <h2>Welcome to React!</h2>;
}

function App() {
  return (
    <div>
      <UserCard />
      <UserCard />
      <UserCard />
    </div>
  );
}

export default App;


Browser output
Welcome to React!
Welcome to React!
Welcome to React!
One component, reused three times.
Notice this:
<UserCard />


We are using the component like an HTML tag.

We don't write:
UserCard()
```

When using components in JSX, write them as tags.

15. Props (properties)
Props are how a parent passes data to a child component. They are read-only (immutable) inside the component.

```javascript
function UserCard({ name, role, avatar }) {
  return (
    <div>
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <p>{role}</p>
    </div>
  );
}
```

- Props are destructured in the parameter list or accessed via `props.name`.
- Default props are assigned with default parameter values:
  ```javascript
  function Button({ label = "Click" }) { return <button>{label}</button>; }
  ```
- A component never modifies its own props — that is the parent's job.

16. State (`useState`)
State lets a component remember values that change over time. Updating state triggers a re-render.

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
}
```

Rules:
- Call `useState` at the top of the function component (not inside loops/conditions).
- State updates are asynchronous — do not rely on the new value immediately.
- When the new state depends on the old state, use the functional form:
  ```javascript
  setCount((prev) => prev + 1);
  ```

17. Component types
- Function components (modern, recommended): plain functions returning JSX.
- Class components: extend `React.Component` with a `render()` method. Still valid but legacy; prefer functions with hooks.

18. Component composition
Components can be nested and composed. Pass other components as children:

```javascript
function Card({ children }) {
  return <div className="card">{children}</div>;
}
```

The `children` prop contains whatever is placed between the opening and closing tags.

19. Event handling
- Event names are camelCase (`onClick`, `onChange`, `onSubmit`).
- Pass a function reference, not call it:
  ```javascript
  <button onClick={handleClick}>   // correct
  <button onClick={handleClick()}> // wrong (calls immediately)
  ```

20. Props validation and defaults
- Use `prop-types` (or TypeScript) to document expected props and catch mistakes:
  ```javascript
  UserCard.propTypes = {
    name: PropTypes.string.isRequired,
    role: PropTypes.string
  };
  ```
- In modern projects, TypeScript is preferred over `prop-types`.

21. Key points summary
- Components are functions that return JSX.
- Name must start with a capital letter.
- Props are immutable; state is mutable and triggers re-render.
- Use `useState`/hooks for interactivity.
- Reuse components by using them as tags (`<UserCard />`).
- Keep components small and single-purpose (single responsibility).
- Component files usually export the component (`export default` or named export).