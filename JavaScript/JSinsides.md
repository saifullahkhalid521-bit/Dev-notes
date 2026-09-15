```javaScript
const date = [
  "2026-10-15", // Future date
  "2026-11-01", // Future date
  "2024-03-20", // Past date 1
  "2026-12-25", // Future date
  "2025-08-05"  // Past date 2
];
const todayC = new Date(); 
const pastDataCheck = date.some(elem => new Date(elem) < todayC);
console.log(pastDataCheck);
```