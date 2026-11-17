# React – Week 9 Notes

## 1. JSX

JSX (JavaScript XML) allows us to write HTML-like code inside JavaScript.

**Example:**

```jsx
const name = "Saifullah";

function App() {
  return <h1>Hello {name}</h1>;
}
```

**Important:** Use `{}` to write JavaScript expressions inside JSX.

### JSX Rules

1. Return only one parent element.

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>Welcome</p>
  </div>
);
```

2. Use `className` instead of `class`.

```jsx
<div className="card">Hello</div>
```

3. Close all tags.

```jsx
<img src="photo.jpg" />
```

4. Use `{}` for JavaScript expressions.

```jsx
<h2>{10 + 20}</h2>
```

5. Use Fragment `<> </>` to group elements without an extra HTML element.

```jsx
<>
  <h1>Hello</h1>
  <p>Welcome</p>
</>
```

## 2. Components

Components are reusable building blocks of a React application.

A component is a JavaScript function that returns JSX.

**Example:**

```jsx
function UserCard() {
  return (
    <div>
      <h2>Saifullah</h2>
      <p>Learning React</p>
    </div>
  );
}

export default UserCard;
```

### Component Rules

1. Component names must start with a capital letter.
2. Components return JSX or `null`.
3. Components can be reused multiple times.

### Reusing Components

```jsx
function App() {
  return (
    <div>
      <UserCard />
      <UserCard />
    </div>
  );
}
```

One component can be used multiple times without writing the same code again.

## 3. Import and Export

**Export:** Makes a component available to other files.

```jsx
export default UserCard;
```

**Import:** Brings a component from another file.

```jsx
import UserCard from "./01-user-card";
```

**Using the imported component:**

```jsx
function App() {
  return <UserCard />;
}
```

### Important Terms

| Term      | Meaning                                |
| --------- | -------------------------------------- |
| JSX       | HTML-like syntax in JavaScript         |
| Component | Reusable UI building block             |
| return    | Returns the UI                         |
| import    | Brings code from another file          |
| export    | Shares code with other files           |
| Fragment  | Groups JSX elements without extra HTML |


* Single Component export example
```JSX
// 1. Component function — naam Capital letter se shuru hota hai
function UserProfile() {
  // 2. JavaScript variables — normal JS
  const name = "Rahul";
  const age = 25;
  const skills = ["JS", "React"];

  // 3. JSX return — ek parent div ke andar sab
  return (
    <div className="profile-card">
      {/* 4. Comment JSX style */}
      <h1>Hello, {name}!</h1>              {/* variable render */}
      <p>Age: {age}</p>                     {/* number render */}
      <p>Next year: {age + 1}</p>           {/* expression */}
      <p>Skills: {skills.join(", ")}</p>    {/* function call */}
      <p>Total skills: {skills.length}</p>  {/* property access */}
    </div>
  );
}

export default UserProfile;
```