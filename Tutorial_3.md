# Node.js Fundamentals Assignment
## Full Stack Website Development I - FSWD101

### Course Information
- **Course Code:** FSWD101
- **Instructor:** YAB Datuk Seri Utama Prof. Dr. Lim Zhi Wei
- **Week:** 3
- **Total Marks:** 100
- **Submission Format:** ZIP file containing all code files and a README.md with explanations

---

<p align="center">
  <img src="KL01.png" alt="KaiLin"  />
</p>


## Instructions
1. Create a new folder named `nodejs-assignment-[your-student-id]`
2. Initialize it as a Node.js project with appropriate `package.json`
3. Complete all 5 questions below
4. Include a `README.md` explaining how to run each solution
5. Submit as a ZIP file

---

## Question 1: Package Management and Project Setup (15 marks)

### Scenario
You are starting a new Node.js project for a local bookstore management system. The project needs to be properly initialized with dependencies for development and production.

### Task
Create a complete Node.js project setup with the following requirements:

**File:** `package.json`

### Expected Output Structure:
```json
{
  "name": "bookstore-management",
  "version": "1.0.0",
  "description": "A Node.js application for managing bookstore inventory",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "jest --coverage"
  },
  "dependencies": {
    // Include at least 3 production dependencies
  },
  "devDependencies": {
    // Include at least 2 development dependencies
  },
  "keywords": ["bookstore", "inventory", "nodejs"],
  "author": "Your Name",
  "license": "MIT"
}
```

### Requirements:
1. **Project Information (5 marks)**
   - Appropriate name, version, and description
   - Correct main entry point
   - Author and license information

2. **Scripts Configuration (5 marks)**
   - `start` script to run the application
   - `dev` script using nodemon for development
   - `test` script for running tests

3. **Dependencies (5 marks)**
   - At least 3 production dependencies (e.g., express, mongoose, dotenv)
   - At least 2 development dependencies (e.g., nodemon, jest)
   - Proper semantic versioning usage

**Deliverable:** Submit `package.json` file with explanation of each dependency choice in README.md

---

## Question 2: File System Operations and Error Handling (25 marks)

### Scenario
You are building a log management system for a web application. The system needs to handle log files, create directories, and manage file operations safely with proper error handling.

### Task
Create a Node.js application called `log-manager.js` that implements the following functionality:

### Expected Functionality:

1. **Directory Management (8 marks)**
   - Create a `logs` directory if it doesn't exist
   - Create subdirectories for different log types: `error`, `info`, `debug`

2. **Log File Operations (12 marks)**
   - Function to write log entries with timestamp
   - Function to read and display log entries
   - Function to clear old logs (files older than 7 days)

3. **Error Handling (5 marks)**
   - Proper error handling for all file operations
   - Meaningful error messages for different failure scenarios

### Expected Output Example:
```
Creating log directory structure...
✓ Created directory: logs
✓ Created directory: logs/error
✓ Created directory: logs/info
✓ Created directory: logs/debug

Writing log entry...
✓ Log entry written to logs/info/2024-07-18.log

Reading log entries...
[2024-07-18 10:30:15] User login successful
[2024-07-18 10:35:22] Database connection established
[2024-07-18 10:40:08] API request processed

Cleaning old logs...
✓ Removed 3 old log files
```

### Required Functions:
```javascript
// Function signatures (implement these)
async function createLogDirectories()
async function writeLogEntry(level, message)
async function readLogEntries(level, date)
async function cleanOldLogs(daysToKeep)
```

**Deliverable:** Submit `log-manager.js` with proper error handling and console output as shown above.

---

## Question 3: HTTP Server and Request Handling (20 marks)

### Scenario
You are developing a simple file server for a local development team. The server should serve static files and provide basic file information through different routes.

### Task
Create an HTTP server (`file-server.js`) that handles the following requirements:

### Expected Routes and Responses:

1. **Static File Serving (10 marks)**
   - Route: `GET /files/<filename>`
   - Serve files from a `public` directory
   - Handle different file types (HTML, CSS, JS, images)
   - Return appropriate Content-Type headers

2. **File Information API (10 marks)**
   - Route: `GET /info/<filename>`
   - Return JSON with file information (size, modified date, type)
   - Handle file not found scenarios

### Expected Output Examples:

**Request:** `GET /files/index.html`
```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 1234

<!DOCTYPE html>
<html>...
```

**Request:** `GET /info/index.html`
```json
{
  "filename": "index.html",
  "size": 1234,
  "modified": "2024-07-18T10:30:15.000Z",
  "type": "text/html",
  "exists": true
}
```

**Request:** `GET /info/nonexistent.txt`
```json
{
  "filename": "nonexistent.txt",
  "exists": false,
  "error": "File not found"
}
```

### Requirements:
- Server should run on port 3000
- Include proper error handling for 404 and 500 errors
- Create a `public` directory with sample files for testing
- Log all requests with timestamp and method

**Deliverable:** Submit `file-server.js` and a `public` directory with at least 3 sample files.

---

## Question 4: Command Line Application (25 marks)

### Scenario
You are creating a command-line tool for a development team to manage their project files. The tool should support various file operations and provide a user-friendly interface.

### Task
Create a CLI application (`file-cli.js`) that supports the following commands:

### Expected Commands and Usage:

1. **File Operations (15 marks)**
   ```bash
   node file-cli.js create <filename> [content]
   node file-cli.js read <filename>
   node file-cli.js update <filename> <new-content>
   node file-cli.js delete <filename>
   ```

2. **Directory Operations (10 marks)**
   ```bash
   node file-cli.js list [directory]
   node file-cli.js mkdir <directory-name>
   ```

### Expected Output Examples:

**Command:** `node file-cli.js create test.txt "Hello World"`
```
✓ File 'test.txt' created successfully with content.
```

**Command:** `node file-cli.js read test.txt`
```
Content of 'test.txt':
Hello World
```

**Command:** `node file-cli.js list`
```
Files in current directory:
📁 node_modules/
📁 public/
📄 file-cli.js
📄 package.json
📄 test.txt
```

**Command:** `node file-cli.js delete nonexistent.txt`
```
❌ Error: File 'nonexistent.txt' not found.
```

### Requirements:
- Use `process.argv` to parse command line arguments
- Implement proper error handling with user-friendly messages
- Support both absolute and relative paths
- Use emojis and colors for better user experience (optional but recommended)
- Include help command that shows usage instructions

**Deliverable:** Submit `file-cli.js` with comprehensive command support and error handling.

---

## Question 5: Asynchronous Programming and Event Loop (15 marks)

### Scenario
You are building a data processing system that needs to handle multiple asynchronous operations efficiently. The system should demonstrate understanding of Node.js event loop and asynchronous patterns.

### Task
Create a Node.js application (`async-processor.js`) that demonstrates different asynchronous programming patterns:

### Expected Functionality:

1. **Callback Pattern (5 marks)**
   - Function to process data using callbacks
   - Demonstrate error-first callback pattern

2. **Promise Pattern (5 marks)**
   - Convert callback-based function to Promise-based
   - Use async/await for cleaner code

3. **Event Loop Demonstration (5 marks)**
   - Show the order of execution for different async operations
   - Include setTimeout, setImmediate, and process.nextTick

### Expected Output Example:
```
Starting async processing demonstration...

=== Callback Pattern ===
Processing data with callbacks...
✓ Data processed successfully: [processed] Hello World

=== Promise Pattern ===
Processing data with promises...
✓ Data processed successfully: [processed] Hello World

=== Event Loop Demonstration ===
1. Start
2. End
3. nextTick callback
4. Promise resolved
5. setImmediate callback
6. setTimeout callback

Processing complete!
```

### Required Functions:
```javascript
// Implement these functions
function processDataCallback(data, callback) { /* callback pattern */ }
function processDataPromise(data) { /* promise pattern */ }
function demonstrateEventLoop() { /* event loop demo */ }
```

### Requirements:
- Demonstrate understanding of callback hell and how to avoid it
- Show proper error handling in both callback and promise patterns
- Include comments explaining the execution order
- Use realistic processing delays (setTimeout) to simulate real async operations

**Deliverable:** Submit `async-processor.js` with clear console output showing execution order and proper async handling.

---

## Submission Guidelines

### File Structure:
```
nodejs-assignment-[student-id]/
├── package.json
├── log-manager.js
├── file-server.js
├── file-cli.js
├── async-processor.js
├── public/
│   ├── index.html
│   ├── style.css
│   └── script.js
├── logs/
└── README.md
```

### README.md Requirements:
- Instructions to run each application
- Explanation of design choices
- Dependencies and their purposes
- Any additional features implemented

### Marking Criteria:
- **Functionality (60%)**: Code works as specified
- **Error Handling (20%)**: Proper error handling and user feedback
- **Code Quality (15%)**: Clean, readable, and well-commented code
- **Documentation (5%)**: Clear README and inline comments

### Submission:
- ZIP file named `nodejs-assignment-[student-id].zip`
- Submit through course management system
- **Due Date:** [Insert due date]

---

## Additional Notes:
- Test your code thoroughly before submission
- Use proper Git commit messages if version control is used
- Include package-lock.json if dependencies are installed
- Ensure all code runs on Node.js version 18 or higher

**Good luck with your assignment!**