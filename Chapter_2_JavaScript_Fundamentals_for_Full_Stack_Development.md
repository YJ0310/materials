# Chapter 2: JavaScript Fundamentals for Full-Stack Development
## Full Stack Website Development I - Smol Tako

### Course Information
- **Course Code:** FSWD101
- **Instructor:** YAB Datuk Seri Utama Prof. Dr. Lim Zhi Wei
- **Chapter Duration:** Week 2
- **Tutorial Assessment:** 2%

---

## Learning Objectives

By the end of this chapter, students will be able to:
- Utilize modern ES6+ JavaScript features in full-stack development
- Implement asynchronous programming patterns effectively
- Work with JavaScript module systems
- Apply advanced JavaScript concepts in real-world scenarios

---

## 1. ES6+ Features

### 1.1 Variable Declarations

**Let and Const**
- `let`: Block-scoped variable declaration
- `const`: Block-scoped constant declaration
- Replaces `var` in modern JavaScript

```javascript
// Old way (var)
var name = "John";
var age = 25;

// Modern way (let/const)
let name = "John";
const age = 25;
```

**Key Differences:**
- `var` is function-scoped, `let` and `const` are block-scoped
- `const` cannot be reassigned
- Temporal dead zone prevents usage before declaration

### 1.2 Arrow Functions

**Syntax:**
```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// With block body
const multiply = (a, b) => {
    const result = a * b;
    return result;
};
```

**Benefits:**
- Concise syntax
- Lexical `this` binding
- Implicit return for single expressions

### 1.3 Template Literals

**String Interpolation:**
```javascript
const name = "Alice";
const age = 30;

// Old way
const message = "Hello, my name is " + name + " and I am " + age + " years old.";

// Template literals
const message = `Hello, my name is ${name} and I am ${age} years old.`;
```

**Multi-line Strings:**
```javascript
const html = `
    <div>
        <h1>${title}</h1>
        <p>${content}</p>
    </div>
`;
```

### 1.4 Destructuring

**Array Destructuring:**
```javascript
const colors = ['red', 'green', 'blue'];
const [primary, secondary, tertiary] = colors;

// With default values
const [first, second, third = 'yellow'] = ['red', 'green'];
```

**Object Destructuring:**
```javascript
const user = {
    name: 'John',
    email: 'john@example.com',
    age: 25
};

const { name, email } = user;

// With renaming
const { name: userName, email: userEmail } = user;
```

### 1.5 Spread and Rest Operators

**Spread Operator (...):**
```javascript
// Array spreading
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];

// Object spreading
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 };
```

**Rest Parameters:**
```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2, 3, 4, 5); // 15
```

### 1.6 Enhanced Object Literals

```javascript
const name = 'John';
const age = 25;

// Shorthand properties
const user = { name, age };

// Method definitions
const calculator = {
    add(a, b) {
        return a + b;
    },
    
    // Computed property names
    [name + 'Method']() {
        return 'Hello';
    }
};
```

---

## 2. Asynchronous Programming

### 2.1 Understanding Asynchronous JavaScript

**The Problem:**
JavaScript is single-threaded, but web applications need to handle multiple operations simultaneously (API calls, file operations, timers).

**Event Loop:**
- Call Stack: Executes synchronous code
- Web APIs: Handle asynchronous operations
- Callback Queue: Holds completed async operations
- Event Loop: Moves callbacks to call stack when empty

### 2.2 Callbacks

**Basic Callback Pattern:**
```javascript
function fetchData(callback) {
    setTimeout(() => {
        const data = { id: 1, name: 'John' };
        callback(data);
    }, 1000);
}

fetchData((result) => {
    console.log(result);
});
```

**Callback Hell:**
```javascript
// Problematic nested callbacks
getData((a) => {
    getMoreData(a, (b) => {
        getMoreData(b, (c) => {
            getMoreData(c, (d) => {
                // This becomes unmanageable
            });
        });
    });
});
```

### 2.3 Promises

**Promise Basics:**
```javascript
const myPromise = new Promise((resolve, reject) => {
    const success = true;
    
    if (success) {
        resolve('Operation successful');
    } else {
        reject('Operation failed');
    }
});

myPromise
    .then(result => console.log(result))
    .catch(error => console.error(error));
```

**Promise Chaining:**
```javascript
fetch('/api/user')
    .then(response => response.json())
    .then(user => fetch(`/api/posts/${user.id}`))
    .then(response => response.json())
    .then(posts => console.log(posts))
    .catch(error => console.error(error));
```

**Promise Utilities:**
```javascript
// Promise.all - All promises must resolve
Promise.all([promise1, promise2, promise3])
    .then(results => console.log(results));

// Promise.race - First promise to settle wins
Promise.race([promise1, promise2])
    .then(result => console.log(result));

// Promise.allSettled - Wait for all, regardless of outcome
Promise.allSettled([promise1, promise2])
    .then(results => console.log(results));
```

### 2.4 Async/Await

**Async Function Declaration:**
```javascript
async function fetchUserData() {
    try {
        const response = await fetch('/api/user');
        const user = await response.json();
        return user;
    } catch (error) {
        console.error('Error fetching user:', error);
        throw error;
    }
}
```

**Error Handling:**
```javascript
async function handleAsyncOperation() {
    try {
        const result1 = await operation1();
        const result2 = await operation2(result1);
        const result3 = await operation3(result2);
        return result3;
    } catch (error) {
        console.error('Error in async operation:', error);
        // Handle error appropriately
    }
}
```

**Parallel Execution:**
```javascript
async function fetchMultipleResources() {
    try {
        // Sequential (slower)
        const user = await fetchUser();
        const posts = await fetchPosts();
        
        // Parallel (faster)
        const [user, posts] = await Promise.all([
            fetchUser(),
            fetchPosts()
        ]);
        
        return { user, posts };
    } catch (error) {
        console.error('Error fetching resources:', error);
    }
}
```

---

## 3. Module Systems

### 3.1 CommonJS (Node.js)

**Exporting:**
```javascript
// math.js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

module.exports = {
    add,
    subtract
};

// Or individual exports
exports.multiply = (a, b) => a * b;
```

**Importing:**
```javascript
// app.js
const { add, subtract } = require('./math');
const math = require('./math');

console.log(add(5, 3)); // 8
console.log(math.subtract(5, 3)); // 2
```

### 3.2 ES6 Modules

**Named Exports:**
```javascript
// utils.js
export function formatDate(date) {
    return date.toISOString();
}

export const API_URL = 'https://api.example.com';

export class User {
    constructor(name) {
        this.name = name;
    }
}
```

**Default Exports:**
```javascript
// database.js
class Database {
    connect() {
        // Connection logic
    }
}

export default Database;
```

**Importing:**
```javascript
// app.js
import Database from './database.js';
import { formatDate, API_URL, User } from './utils.js';

// Import all as namespace
import * as utils from './utils.js';

// Dynamic imports
const module = await import('./dynamicModule.js');
```

### 3.3 Module Best Practices

**File Organization:**
```
src/
├── components/
│   ├── Header.js
│   ├── Footer.js
│   └── index.js
├── utils/
│   ├── dateHelpers.js
│   ├── apiHelpers.js
│   └── index.js
├── services/
│   ├── userService.js
│   └── postService.js
└── app.js
```

**Barrel Exports:**
```javascript
// components/index.js
export { default as Header } from './Header.js';
export { default as Footer } from './Footer.js';

// Usage
import { Header, Footer } from './components';
```

---

## 4. Advanced JavaScript Concepts

### 4.1 Closures

**Definition:**
A closure is a function that has access to variables in its outer (enclosing) scope even after the outer function has returned.

```javascript
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

**Practical Applications:**
```javascript
// Module pattern
const calculator = (function() {
    let result = 0;
    
    return {
        add: (x) => result += x,
        subtract: (x) => result -= x,
        getResult: () => result,
        reset: () => result = 0
    };
})();
```

### 4.2 Higher-Order Functions

**Functions that take other functions as arguments:**
```javascript
function processArray(arr, processor) {
    return arr.map(processor);
}

const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, x => x * 2);
```

**Common Higher-Order Functions:**
```javascript
// Array methods
const users = [
    { name: 'John', age: 25 },
    { name: 'Jane', age: 30 },
    { name: 'Bob', age: 35 }
];

// Filter
const adults = users.filter(user => user.age >= 18);

// Map
const names = users.map(user => user.name);

// Reduce
const totalAge = users.reduce((sum, user) => sum + user.age, 0);

// Find
const john = users.find(user => user.name === 'John');
```

### 4.3 Prototypes and Classes

**Prototype Chain:**
```javascript
function Person(name) {
    this.name = name;
}

Person.prototype.greet = function() {
    return `Hello, I'm ${this.name}`;
};

const john = new Person('John');
console.log(john.greet()); // "Hello, I'm John"
```

**ES6 Classes:**
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    static fromString(str) {
        const [name, age] = str.split(',');
        return new Person(name, parseInt(age));
    }
}

class Employee extends Person {
    constructor(name, age, position) {
        super(name, age);
        this.position = position;
    }
    
    greet() {
        return `${super.greet()}, I work as a ${this.position}`;
    }
}
```

---

## 5. Error Handling

### 5.1 Try-Catch-Finally

```javascript
function parseJSON(jsonString) {
    try {
        const data = JSON.parse(jsonString);
        return data;
    } catch (error) {
        console.error('Invalid JSON:', error.message);
        return null;
    } finally {
        console.log('JSON parsing attempted');
    }
}
```

### 5.2 Custom Error Classes

```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = 'ValidationError';
    }
}

function validateEmail(email) {
    if (!email.includes('@')) {
        throw new ValidationError('Invalid email format');
    }
}

try {
    validateEmail('invalid-email');
} catch (error) {
    if (error instanceof ValidationError) {
        console.log('Validation failed:', error.message);
    } else {
        console.log('Unexpected error:', error);
    }
}
```

---

## 6. Practical Examples for Full-Stack Development

### 6.1 API Client with Async/Await

```javascript
class ApiClient {
    constructor(baseURL) {
        this.baseURL = baseURL;
    }
    
    async get(endpoint) {
        try {
            const response = await fetch(`${this.baseURL}${endpoint}`);
            if (!response.ok) {
                throw new Error(`HTTP error! status: ${response.status}`);
            }
            return await response.json();
        } catch (error) {
            console.error('API request failed:', error);
            throw error;
        }
    }
    
    async post(endpoint, data) {
        try {
            const response = await fetch(`${this.baseURL}${endpoint}`, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            });
            return await response.json();
        } catch (error) {
            console.error('API request failed:', error);
            throw error;
        }
    }
}

// Usage
const api = new ApiClient('https://api.example.com');

async function loadUserData() {
    try {
        const user = await api.get('/user/123');
        const posts = await api.get(`/user/${user.id}/posts`);
        return { user, posts };
    } catch (error) {
        console.error('Failed to load user data:', error);
    }
}
```

### 6.2 Utility Functions with Modern JavaScript

```javascript
// debounce.js
export function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => func.apply(this, args), delay);
    };
}

// validation.js
export const validators = {
    email: (email) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email),
    password: (password) => password.length >= 8,
    required: (value) => value !== null && value !== undefined && value !== ''
};

// arrayHelpers.js
export function groupBy(array, key) {
    return array.reduce((groups, item) => {
        const group = item[key];
        groups[group] = groups[group] || [];
        groups[group].push(item);
        return groups;
    }, {});
}

export function uniqueBy(array, key) {
    const seen = new Set();
    return array.filter(item => {
        const value = item[key];
        if (seen.has(value)) {
            return false;
        }
        seen.add(value);
        return true;
    });
}
```

---

## Key Takeaways

1. **Modern JavaScript features** like arrow functions, destructuring, and template literals make code more readable and maintainable
2. **Asynchronous programming** with Promises and async/await is essential for handling API calls and other async operations
3. **Module systems** help organize code and manage dependencies effectively
4. **Advanced concepts** like closures and higher-order functions enable powerful programming patterns
5. **Error handling** is crucial for building robust applications
6. These fundamentals form the foundation for both frontend (React) and backend (Node.js) development

---

## Next Steps

In the next chapter, we'll explore Node.js fundamentals and see how these JavaScript concepts apply to server-side development. The tutorial for this chapter will focus on implementing advanced JavaScript concepts in practical scenarios.

---

## Additional Resources

- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info](https://javascript.info/)
- [You Don't Know JS book series](https://github.com/getify/You-Dont-Know-JS)
- [Async JavaScript documentation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous)