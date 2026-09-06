# Fetch()

### Simple Definition:
fetch() ek browser function hai jo network requests (API calls) bhejne ke kaam aata hai. Yeh Promise return karta hai, isliye hum iske saath .then() ya async/await use kar sakte hain.

* Real-World Analogy:

1. Aap restaurant mein order karte ho (request)

2. Waiter kitchen mein jaata hai (network call)

3. Khana aata hai (response)

4. Agar khana nahi aata toh problem hoti hai (error)

### Basic Syntax:

```javascript
// GET Request (Data lana)
fetch('URL')              // Step 1: Request bhejo
    .then(response => {   // Step 2: Response aaya
        // response object mein status, headers, body sab kuch hai
        return response.json(); // Step 3: Body ko JSON mein convert karo
    })
    .then(data => {       // Step 4: Converted data use karo
        console.log(data);
    })
    .catch(error => {     // Step 5: Agar kuch galat ho
        console.log('Error:', error);
    });
```
### Important: Response Object ke Properties

```javascript
fetch('https://api.github.com/users/octocat')
    .then(response => {
        console.log(response.status);      // 200 (OK), 404 (Not Found), 500 (Server Error)
        console.log(response.ok);          // true if status 200-299, false otherwise
        console.log(response.headers);     // Headers (content-type, etc.)
        
        // IMPORTANT: response.body ko directly use nahi kar sakte
        // Pehle convert karna padta hai:
        return response.json();            // JSON data ke liye
        // OR
        return response.text();            // Plain text ke liye
        // OR
        return response.blob();            // Image/file ke liye
    })
    .then(data => {
        console.log(data);
    });

    //response.formData()	Jab form data submit karna ho	File uploads
```

## Different Types of Requests
1. GET: Data fetch karne ke liye
2. POST: Naya data create karne ke liye
3. PUT: Existing data update karne ke liye
4. DELETE: Data delete karne ke liye

### 1. GET Request (Data Lana)
```javascript
// Simple GET - Data lana
fetch('https://api.github.com/users/octocat')
    .then(res => res.json())
    .then(data => {
        console.log('Name:', data.name);
        console.log('Bio:', data.bio);
        console.log('Followers:', data.followers);
    })
    .catch(err => console.log('Error:', err));
   ```

### 2. POST Request (Data Create Karna)
```javascript
// POST - Naya user create karna
const newUser = {
    name: 'Rahul Kumar',
    email: 'rahul@example.com',
    age: 25
};

fetch('https://jsonplaceholder.typicode.com/users', {
    method: 'POST',                    // Request type
    headers: {
        'Content-Type': 'application/json',  // Data type batana
    },
    body: JSON.stringify(newUser)      // Data ko JSON string mein convert
})
.then(res => res.json())
.then(data => {
    console.log('User Created:', data);
})
.catch(err => console.log('Error:', err));
```


### 3. PUT Request (Update Karna)
```javascript
// PUT - Existing user update karna
const updatedUser = {
    name: 'Rahul Sharma',
    email: 'rahul.sharma@example.com'
};

fetch('https://jsonplaceholder.typicode.com/users/1', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(updatedUser)
})
.then(res => res.json())
.then(data => console.log('Updated:', data))
.catch(err => console.log('Error:', err));
```

### 4. DELETE Request (Data Delete Karna)
```javascript
// DELETE - User delete karna
fetch('https://jsonplaceholder.typicode.com/users/1', {
    method: 'DELETE'
})
.then(res => {
    if (res.status === 200) {
        console.log('User Deleted Successfully');
    } else {
        console.log('Delete Failed');
    }
})
.catch(err => console.log('Error:', err));
```

### Headers Role

* Headers are used to provide additional information about the request or response. For example, the `Content-Type` header is used to specify the type of data being sent in the request body.

```javascript
// Headers - Authentication, Content-Type, etc.

fetch('https://api.github.com/user', {
    headers: {
        'Authorization': 'Bearer YOUR_TOKEN_HERE',  // Authentication
        'Content-Type': 'application/json',        // Data type
        'Accept': 'application/json'               // Response type
    }
})
.then(res => res.json())
.then(data => console.log(data))
.catch(err => console.log('Error:', err));
```

### Error Handling - 🔴 CORE

```javascript
// fetch() sirf network errors par reject karta hai
// 404, 500 par reject nahi karta - isliye humein manually handle karna padta hai

fetch('https://api.github.com/users/unknownuser12345')
    .then(response => {
        if (!response.ok) {  // Agar status 200-299 nahi hai
            throw new Error(`HTTP Error: ${response.status}`);
        }
        return response.json();
    })
    .then(data => {
        console.log('Success:', data);
    })
    .catch(error => {
        console.log('Network or HTTP Error:', error.message);
    });
```

### Async/Await Version (Tumhare liye important)
```javascript
// Yeh tumhe abhi seekhna hai - yeh cleaner hai

async function getGitHubUser() {
    try {
        const response = await fetch('https://api.github.com/users/octocat');
        
        if (!response.ok) {
            throw new Error(`HTTP Error: ${response.status}`);
        }
        
        const data = await response.json();
        console.log('Name:', data.name);
        console.log('Bio:', data.bio);
        return data;
    } catch (error) {
        console.log('Error:', error.message);
    }
}

// Call karo
getGitHubUser();
```


### Common Pitfalls (Galtiyan) - Avoid Karein

```javascript
// ❌ GALT: Response ko directly use karna
fetch('https://api.github.com/users/octocat')
    .then(response => {
        console.log(response);  // Yeh raw response hai, data nahi
    });

// ✅ SAHI: Response ko convert karo
fetch('https://api.github.com/users/octocat')
    .then(response => response.json())
    .then(data => console.log(data));

// ❌ GALT: 404/500 errors ko catch na karna
fetch('https://api.github.com/users/invalid')
    .then(response => response.json())  // 404 par bhi yeh chalega
    .then(data => console.log(data));

// ✅ SAHI: response.ok check karo
fetch('https://api.github.com/users/invalid')
    .then(response => {
        if (!response.ok) {
            throw new Error('User not found');
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(err => console.log('Error:', err.message));
  ```


## Common Use Cases in Real Projects
```javascript

// 1. Form Submit Karna
javascript
async function submitForm(formData) {
    try {
        const response = await fetch('https://api.example.com/submit', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(formData)
        });
        
        if (!response.ok) throw new Error('Submission Failed');
        
        const result = await response.json();
        console.log('Form Submitted:', result);
    } catch (error) {
        console.log('Error:', error);
    }
}


// 2. Multiple APIs Se Data Lana
javascript
async function getDashboardData() {
    try {
        const [user, posts, comments] = await Promise.all([
            fetch('https://jsonplaceholder.typicode.com/users/1').then(r => r.json()),
            fetch('https://jsonplaceholder.typicode.com/posts').then(r => r.json()),
            fetch('https://jsonplaceholder.typicode.com/comments').then(r => r.json())
        ]);
        
        console.log('Dashboard Data:', { user, posts, comments });
        return { user, posts, comments };
    } catch (error) {
        console.log('Error fetching dashboard data:', error);
    }
}


// 3. Loading States ke Saath
javascript
async function fetchUserWithLoading() {
    console.log('Loading...');  // Loading state
    
    try {
        const response = await fetch('https://api.github.com/users/octocat');
        const data = await response.json();
        console.log('Data Loaded:', data);
        return data;
    } catch (error) {
        console.log('Error:', error);
    } finally {
        console.log('Loading Complete');  // Always runs
    }
}
```