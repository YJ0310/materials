# Full Stack Website Development I (FSWD101)
## Chapter 2 Assignment: JavaScript Fundamentals for Full-Stack Development

**Course:** Full Stack Website Development I  
**Organization:** Smol Tako  
**Instructor:** YAB Datuk Seri Utama Prof. Dr. Lim Zhi Wei  
**Total Marks:** 100  
**Duration:** 3 hours  
**Due Date:** [To be announced by instructor]

---

## Instructions
- Answer all questions
- Write clean, well-commented code
- Test your code before submission
- Submit all files in a single ZIP folder named `StudentID_Chapter2_Assignment`
- Late submissions will be penalized according to course policy

---

### Question 1: ES6+ Features Implementation (20 marks)

**Part A (10 marks):** Create a JavaScript file that demonstrates the following ES6+ features:

1. **Arrow Functions (2 marks):** Write three different arrow functions:
   - A simple arrow function that returns the square of a number
   - An arrow function with multiple parameters that calculates the area of a rectangle
   - An arrow function that uses implicit return to double an array of numbers

2. **Template Literals (2 marks):** Create a function that takes a user object (name, age, email) and returns a formatted string using template literals.

3. **Destructuring (3 marks):** 
   - Demonstrate array destructuring with at least 5 elements
   - Demonstrate object destructuring with nested objects
   - Use destructuring in function parameters

4. **Spread and Rest Operators (3 marks):**
   - Use spread operator to merge two arrays
   - Use rest operator in a function that accepts unlimited parameters
   - Use spread operator to clone an object

**Part B (10 marks):** Create a class called `Student` using ES6 class syntax that includes:
- Constructor with parameters: name, age, courses (array)
- Method to add a course
- Method to remove a course
- Method to get student info using template literals
- Static method to compare two students' ages
- Create two instances and demonstrate all methods

---

### Question 2: Asynchronous Programming Mastery (25 marks)

**Part A: Promises (10 marks)**
Create a file that demonstrates:
1. A function that returns a Promise which resolves after 2 seconds with a success message
2. A function that returns a Promise which rejects with an error message
3. Use `.then()` and `.catch()` to handle both promises
4. Demonstrate `Promise.all()` with at least 3 promises
5. Demonstrate `Promise.race()` with at least 2 promises

**Part B: Async/Await (10 marks)**
Convert the Promise-based code from Part A to use async/await syntax:
1. Create async functions that handle the promises from Part A
2. Implement proper error handling using try/catch blocks
3. Create a function that simulates fetching user data with a delay
4. Chain multiple async operations together

**Part C: Real-world Simulation (5 marks)**
Create a simulation of a simple API call system:
- Function to simulate fetching user data (returns user object after delay)
- Function to simulate fetching user posts (returns array of posts after delay)
- Function to simulate fetching post comments (returns array of comments after delay)
- Chain these operations using async/await to get a complete user profile

---

### Question 3: Advanced Array and Object Manipulation (20 marks)

Create a JavaScript application that manages a library system with the following requirements:

**Data Structure (5 marks):**
Create an array of book objects, each containing:
- id, title, author, genre, publishedYear, isAvailable, borrowedBy (if applicable)

**Implementation (15 marks):**
1. **Filter Operations (5 marks):**
   - Function to get all available books
   - Function to get books by genre
   - Function to get books published after a specific year

2. **Map Operations (5 marks):**
   - Function to get all book titles
   - Function to format book information for display
   - Function to create a summary report of all books

3. **Reduce Operations (5 marks):**
   - Function to count total books by genre
   - Function to calculate average publication year
   - Function to find the most borrowed genre

Use appropriate ES6+ features including arrow functions, destructuring, and template literals.

---

### Question 4: Module Systems and Code Organization (15 marks)

Create a modular calculator application with the following structure:

**Part A: Module Creation (10 marks)**
1. **mathUtils.js (5 marks):** Create a module that exports:
   - Basic arithmetic functions (add, subtract, multiply, divide)
   - Advanced functions (power, square root, factorial)
   - Use both named exports and default export

2. **constants.js (2 marks):** Create a module that exports:
   - Mathematical constants (PI, E, GOLDEN_RATIO)
   - Configuration constants (MAX_PRECISION, DEFAULT_DECIMAL_PLACES)

3. **main.js (3 marks):** Create the main file that:
   - Imports functions from mathUtils.js using various import syntaxes
   - Imports constants from constants.js
   - Demonstrates the usage of all imported functions and constants

**Part B: Module Patterns (5 marks)**
Demonstrate understanding of different module patterns:
1. CommonJS syntax (require/module.exports)
2. ES6 Module syntax (import/export)
3. Mixed imports (default and named imports in one statement)

---

### Question 5: Comprehensive Application Development (20 marks)

Create a **Task Management System** that demonstrates all concepts from Chapter 2:

**Requirements:**
1. **Task Class (5 marks):**
   - Use ES6 class syntax
   - Properties: id, title, description, priority, status, createdDate, dueDate
   - Methods: markComplete, updatePriority, isOverdue
   - Static method to compare task priorities

2. **TaskManager Class (8 marks):**
   - Manage an array of tasks
   - Methods using array methods (map, filter, reduce):
     - addTask (with validation)
     - deleteTask
     - updateTask
     - getTasks (with filtering options)
     - getTaskStats (using reduce)
     - getOverdueTasks
     - getTasksByPriority

3. **Asynchronous Operations (4 marks):**
   - Simulate saving tasks to a database (async function with delay)
   - Simulate loading tasks from a database (async function with delay)
   - Implement proper error handling

4. **Module Organization (3 marks):**
   - Separate Task and TaskManager into different modules
   - Create a main file that imports and uses both classes
   - Demonstrate the complete functionality

**Bonus Features (Additional 5 marks):**
- Implement task search functionality using regex
- Add task categories with filtering
- Implement task sorting by different criteria
- Add input validation using custom error classes

---

## Submission Requirements

1. **File Structure:**
   ```
   StudentID_Chapter2_Assignment/
   ├── question1/
   │   ├── es6-features.js
   │   └── student-class.js
   ├── question2/
   │   ├── promises.js
   │   ├── async-await.js
   │   └── api-simulation.js
   ├── question3/
   │   └── library-system.js
   ├── question4/
   │   ├── mathUtils.js
   │   ├── constants.js
   │   └── main.js
   ├── question5/
   │   ├── Task.js
   │   ├── TaskManager.js
   │   └── main.js
   └── README.md
   ```

2. **README.md file** containing:
   - Your name and student ID
   - Brief description of each question's solution
   - Instructions on how to run each file
   - Any assumptions made
   - Challenges faced and how you overcame them

3. **Code Quality Requirements:**
   - Proper indentation and formatting
   - Meaningful variable and function names
   - Comprehensive comments explaining complex logic
   - Error handling where appropriate
   - Testing of all functions with sample data

---

## Marking Rubric

| Criteria | Excellent (90-100%) | Good (80-89%) | Satisfactory (70-79%) | Needs Improvement (60-69%) | Unsatisfactory (0-59%) |
|----------|-------------------|---------------|----------------------|---------------------------|------------------------|
| **Code Functionality** | All requirements met, code runs perfectly | Most requirements met, minor issues | Basic requirements met, some issues | Some requirements met, several issues | Requirements not met, major issues |
| **ES6+ Features Usage** | Excellent use of modern JavaScript features | Good use of ES6+ features | Basic use of modern features | Limited use of ES6+ features | Poor or no use of modern features |
| **Code Quality** | Clean, well-structured, well-commented | Good structure and comments | Adequate structure | Poor structure, minimal comments | Very poor code quality |
| **Error Handling** | Comprehensive error handling | Good error handling | Basic error handling | Limited error handling | No error handling |
| **Documentation** | Excellent documentation and README | Good documentation | Basic documentation | Limited documentation | Poor or no documentation |

---

**Good luck with your assignment! Remember to start early and test your code thoroughly.**