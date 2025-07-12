# Full Stack Website Development I (FSWD101)

![Cover](SaveClip.App_AQOXhLwqTA23AZJxxI2bO3c7_uK8RpP2sdz0YegxIrj0N1zn-S8h-_9NqivmACbmyoG-xv0yMhpXIxa2_J4Prk0Je3D57a7Sd8HSU_U.mp4)
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

### Question 1: Online Shopping Cart System - ES6+ Features (20 marks)

**Scenario:** You are developing an online shopping cart system for "Smol Tako Electronics Store". The system needs to handle product information and customer data efficiently using modern JavaScript features.

**Given Data:**
```javascript
const products = [
    { id: 1, name: "Laptop", price: 2500, category: "Electronics", inStock: true },
    { id: 2, name: "Mouse", price: 50, category: "Electronics", inStock: true },
    { id: 3, name: "Keyboard", price: 120, category: "Electronics", inStock: false },
    { id: 4, name: "Monitor", price: 800, category: "Electronics", inStock: true }
];

const customer = {
    id: 101,
    name: "Ahmad Rahman",
    email: "ahmad@example.com",
    address: {
        street: "123 Jalan Utama",
        city: "Petaling Jaya",
        postcode: "47800",
        state: "Selangor"
    },
    preferences: ["Electronics", "Books"]
};
```

**Part A: Arrow Functions and Template Literals (10 marks)**

1. **Create arrow functions (4 marks):**
   - `calculateTax` - takes price and tax rate (0.06 for 6% SST), returns tax amount
   - `calculateTotal` - takes price and tax, returns total price
   - `formatPrice` - takes a number, returns formatted string "RM 2,500.00"

2. **Create a customer greeting function (3 marks):**
   - Function name: `generateWelcomeMessage`
   - Uses template literals to create a personalized message
   - **Expected Output:** `"Welcome back, Ahmad Rahman! Your last order was delivered to 123 Jalan Utama, Petaling Jaya, Selangor 47800"`

3. **Create a product summary function (3 marks):**
   - Function name: `createProductSummary`
   - Takes a product object and returns a formatted string using template literals
   - **Expected Output for Laptop:** `"Laptop - RM 2,500.00 (Electronics) - In Stock"`

**Part B: Destructuring and Modern Object Features (10 marks)**

4. **Implement destructuring functions (6 marks):**
   - `extractCustomerInfo` - uses object destructuring to extract name, email, and city from customer object
   - `getTopProducts` - uses array destructuring to get first 2 products from products array
   - **Expected Output:**
     ```javascript
     // extractCustomerInfo(customer)
     { name: "Ahmad Rahman", email: "ahmad@example.com", city: "Petaling Jaya" }
     
     // getTopProducts(products)
     [
         { id: 1, name: "Laptop", price: 2500, category: "Electronics", inStock: true },
         { id: 2, name: "Mouse", price: 50, category: "Electronics", inStock: true }
     ]
     ```

5. **Implement spread operator functions (4 marks):**
   - `addToCart` - takes existing cart array and new product, returns new cart using spread operator
   - `updateCustomerInfo` - takes customer object and updates object, returns new customer object using spread operator
   - **Expected Output:**
     ```javascript
     // addToCart([product1], product2)
     [product1, product2]
     
     // updateCustomerInfo(customer, { phone: "012-3456789" })
     // Returns customer object with added phone field
     ```

---

### Question 2: Restaurant Order Processing System - Asynchronous Programming (25 marks)

**Scenario:** You are building an order processing system for "Restoran Smol Tako". The system needs to simulate cooking time, order preparation, and delivery tracking using asynchronous programming.

**Part A: Promise-based Kitchen Operations (10 marks)**

Create the following functions that return promises:

1. **`prepareIngredients(dishName)`** - Simulates ingredient preparation
   - Takes 1 second to resolve
   - Resolves with: `"Ingredients ready for [dishName]"`
   - Rejects with: `"Ingredients not available for [dishName]"` (20% chance)

2. **`cookDish(dishName)`** - Simulates cooking
   - Takes 3 seconds to resolve
   - Resolves with: `"[dishName] is ready!"`
   - Rejects with: `"Cooking failed for [dishName]"` (10% chance)

3. **`packageOrder(dishName)`** - Simulates packaging
   - Takes 0.5 seconds to resolve
   - Resolves with: `"[dishName] packaged and ready for delivery"`

**Expected Console Output:**
```
Ingredients ready for Nasi Lemak
Nasi Lemak is ready!
Nasi Lemak packaged and ready for delivery
```

**Part B: Async/Await Order Management (10 marks)**

4. **Create `processOrder(dishName)` function (6 marks):**
   - Use async/await to chain the three operations above
   - Implement proper error handling with try/catch
   - Log each step's result
   - **Expected Output:**
     ```
     Processing order for Nasi Lemak...
     ✓ Ingredients ready for Nasi Lemak
     ✓ Nasi Lemak is ready!
     ✓ Nasi Lemak packaged and ready for delivery
     Order completed for Nasi Lemak!
     ```

5. **Create `processMultipleOrders(orders)` function (4 marks):**
   - Takes an array of dish names
   - Process all orders simultaneously using Promise.all
   - Handle errors gracefully
   - **Expected Output:**
     ```javascript
     // processMultipleOrders(["Nasi Lemak", "Mee Goreng", "Teh Tarik"])
     // Should process all orders at the same time and show completion message
     ```

**Part C: Delivery Tracking System (5 marks)**

6. **Create `trackDelivery(orderID)` function:**
   - Simulates delivery tracking with 3 stages: "Picked up", "On the way", "Delivered"
   - Each stage takes 2 seconds
   - Use async/await with a loop
   - **Expected Output:**
     ```
     Order #12345: Picked up
     Order #12345: On the way
     Order #12345: Delivered
     ```

---

### Question 3: University Student Management System - Array Methods (20 marks)

**Scenario:** You are developing a student management system for "Universiti Smol Tako". The system needs to analyze student performance, course enrollment, and generate reports.

**Given Data:**
```javascript
const students = [
    { id: 1, name: "Siti Aminah", age: 20, course: "Computer Science", gpa: 3.8, year: 2, fees: 15000 },
    { id: 2, name: "Raj Kumar", age: 19, course: "Information Technology", gpa: 3.2, year: 1, fees: 12000 },
    { id: 3, name: "Chen Wei Ming", age: 21, course: "Computer Science", gpa: 3.9, year: 3, fees: 18000 },
    { id: 4, name: "Fatimah Zahra", age: 22, course: "Business Administration", gpa: 3.5, year: 4, fees: 20000 },
    { id: 5, name: "David Tan", age: 20, course: "Information Technology", gpa: 2.8, year: 2, fees: 15000 },
    { id: 6, name: "Nurul Iman", age: 19, course: "Computer Science", gpa: 3.7, year: 1, fees: 12000 }
];
```

**Requirements:**

1. **Honor Roll Students (5 marks)**
   - Function: `getHonorRollStudents()`
   - Find students with GPA >= 3.5
   - **Expected Output:**
     ```javascript
     [
         { id: 1, name: "Siti Aminah", age: 20, course: "Computer Science", gpa: 3.8, year: 2, fees: 15000 },
         { id: 3, name: "Chen Wei Ming", age: 21, course: "Computer Science", gpa: 3.9, year: 3, fees: 18000 },
         { id: 6, name: "Nurul Iman", age: 19, course: "Computer Science", gpa: 3.7, year: 1, fees: 12000 }
     ]
     ```

2. **Course Enrollment Report (5 marks)**
   - Function: `generateCourseReport()`
   - Create a summary of students per course with their names
   - **Expected Output:**
     ```javascript
     {
         "Computer Science": ["Siti Aminah", "Chen Wei Ming", "Nurul Iman"],
         "Information Technology": ["Raj Kumar", "David Tan"],
         "Business Administration": ["Fatimah Zahra"]
     }
     ```

3. **Financial Analysis (5 marks)**
   - Function: `calculateFinancialSummary()`
   - Calculate total fees, average fees, and highest fee payer
   - **Expected Output:**
     ```javascript
     {
         totalFees: 92000,
         averageFees: 15333.33,
         highestFeePayer: "Fatimah Zahra"
     }
     ```

4. **Student Performance Report (5 marks)**
   - Function: `generatePerformanceReport()`
   - Create a formatted report showing each student's status
   - Students with GPA >= 3.5 are "Excellent", >= 3.0 are "Good", < 3.0 are "Needs Improvement"
   - **Expected Output:**
     ```javascript
     [
         "Siti Aminah (Year 2, Computer Science): Excellent (GPA: 3.8)",
         "Raj Kumar (Year 1, Information Technology): Good (GPA: 3.2)",
         "Chen Wei Ming (Year 3, Computer Science): Excellent (GPA: 3.9)",
         "Fatimah Zahra (Year 4, Business Administration): Excellent (GPA: 3.5)",
         "David Tan (Year 2, Information Technology): Needs Improvement (GPA: 2.8)",
         "Nurul Iman (Year 1, Computer Science): Excellent (GPA: 3.7)"
     ]
     ```

---

### Question 4: E-commerce API Module System (15 marks)

**Scenario:** You are building a modular e-commerce API system for "Smol Tako Marketplace". The system needs to be organized into separate modules for better maintainability.

**Part A: Create Product Management Module (8 marks)**

1. **File: `productManager.js`**
   - Create a `Product` class with properties: id, name, price, category, stock
   - Create functions:
     - `addProduct(product)` - adds product to inventory
     - `updateStock(productId, quantity)` - updates product stock
     - `getProductsByCategory(category)` - filters products by category
     - `calculateInventoryValue()` - calculates total inventory value
   - Export both the class and functions

2. **File: `constants.js`**
   - Export categories: `CATEGORIES = ["Electronics", "Clothing", "Books", "Home"]`
   - Export tax rates: `TAX_RATES = { SST: 0.06, SERVICE: 0.10 }`
   - Export minimum stock alert: `MIN_STOCK_ALERT = 5`

**Part B: Create Order Processing Module (7 marks)**

3. **File: `orderManager.js`**
   - Import productManager and constants
   - Create `Order` class with properties: id, customerId, products, total, status
   - Create functions:
     - `createOrder(customerId, products)` - creates new order and updates stock
     - `calculateOrderTotal(products)` - calculates total including tax
     - `getOrdersByStatus(status)` - filters orders by status
   - Export the class and functions

4. **File: `main.js`**
   - Import all modules
   - Create sample data and demonstrate all functionality
   - **Expected Console Output:**
     ```
     Product added: Laptop (ID: 1)
     Product added: Phone (ID: 2)
     Order created: Order #1001 for Customer #501
     Order Total: RM 2,756.00 (including taxes)
     Low stock alert: Phone (Stock: 3)
     ```

---

### Question 5: COVID-19 Contact Tracing System - Comprehensive Application (20 marks)

**Scenario:** You are developing a contact tracing system for "Smol Tako Health Ministry". The system needs to track people, their visits to locations, and identify potential contacts efficiently.

**Given Requirements:**
- Track individuals and their health status
- Record location visits with timestamps
- Identify potential contacts based on location and time overlap
- Generate health reports and alerts

**Part A: Person and Location Classes (8 marks)**

1. **Create `Person` class:**
   - Properties: id, name, phone, healthStatus ("healthy", "infected", "recovered"), lastTested
   - Methods: `updateHealthStatus()`, `isHighRisk()`, `getDaysSinceTest()`

2. **Create `Location` class:**
   - Properties: id, name, type, address, maxCapacity
   - Methods: `checkCapacity()`, `addVisit()`, `getVisitsToday()`

**Expected Usage:**
```javascript
const person1 = new Person(1, "Ahmad Ali", "012-3456789", "healthy", "2024-01-15");
const location1 = new Location(1, "Restoran ABC", "restaurant", "KL", 50);
console.log(person1.getDaysSinceTest()); // Should calculate days from lastTested to today
```

**Part B: Contact Tracing Manager (12 marks)**

3. **Create `ContactTracer` class:**
   - Properties: people, locations, visits, alerts
   - Methods:
     - `addPerson(person)` - adds person to system
     - `recordVisit(personId, locationId, timestamp, duration)` - records a visit
     - `findContacts(personId, days)` - finds people who visited same locations within timeframe
     - `generateHealthReport()` - creates summary of health status
     - `identifyHotspots()` - finds locations with most infected visits

4. **Implement asynchronous notification system:**
   - `sendHealthAlert(personId, message)` - simulates sending SMS alert (2 second delay)
   - `processContactTracing(infectedPersonId)` - finds contacts and sends alerts to all

**Expected Output for Contact Tracing:**
```javascript
// When person ID 1 is marked as infected
const tracer = new ContactTracer();
await tracer.processContactTracing(1);

// Expected console output:
// Finding contacts for Ahmad Ali...
// Contact found: Siti Rahman (visited same location within 2 days)
// Contact found: Chen Wei (visited same location within 2 days)
// Sending alert to Siti Rahman...
// Sending alert to Chen Wei...
// Contact tracing completed for Ahmad Ali
```

**Expected Output for Health Report:**
```javascript
tracer.generateHealthReport();

// Expected output:
{
    totalPeople: 15,
    healthy: 12,
    infected: 2,
    recovered: 1,
    highRiskLocations: ["Restoran ABC", "Shopping Mall XYZ"],
    alertsSent: 8
}
```

---

## Submission Requirements

1. **File Structure:**
   ```
   StudentID_Chapter2_Assignment/
   ├── question1/
   │   └── shopping-cart.js
   ├── question2/
   │   └── restaurant-orders.js
   ├── question3/
   │   └── student-management.js
   ├── question4/
   │   ├── productManager.js
   │   ├── orderManager.js
   │   ├── constants.js
   │   └── main.js
   ├── question5/
   │   ├── Person.js
   │   ├── Location.js
   │   ├── ContactTracer.js
   │   └── main.js
   └── README.md
   ```

2. **Testing Requirements:**
   - Each file must include test cases that demonstrate the expected outputs
   - Include console.log statements to show results
   - Test both success and error scenarios

3. **README.md must include:**
   - Your name and student ID
   - How to run each question
   - Sample inputs and expected outputs for each function
   - Any assumptions made

---

## Marking Rubric

| Question | Functionality (60%) | Code Quality (20%) | Expected Output (20%) |
|----------|-------------------|-------------------|---------------------|
| Q1 (20 marks) | Functions work correctly | Clean ES6+ syntax | Matches expected output exactly |
| Q2 (25 marks) | Promises/async work properly | Proper error handling | Console output matches requirements |
| Q3 (20 marks) | Array methods used correctly | Efficient algorithms | Output format matches specification |
| Q4 (15 marks) | Modules export/import correctly | Good separation of concerns | Demonstrates all functionality |
| Q5 (20 marks) | Complete system functionality | Object-oriented design | Realistic simulation output |

**Note:** Partial marks will be awarded for partially correct solutions. Code that doesn't run will receive maximum 30% marks.