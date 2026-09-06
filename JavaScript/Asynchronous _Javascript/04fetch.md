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
