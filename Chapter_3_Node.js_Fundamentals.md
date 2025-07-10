# Chapter 3: Node.js Fundamentals
## Full Stack Website Development I - Smol Tako

### Course Information
- **Course Code:** FSWD101
- **Instructor:** YAB Datuk Seri Utama Prof. Dr. Lim Zhi Wei
- **Week:** 3

---

## Learning Objectives
By the end of this chapter, students will be able to:
- Understand Node.js architecture and its event-driven nature
- Manage packages using NPM (Node Package Manager)
- Perform file system operations using Node.js built-in modules
- Build basic Node.js applications
- Understand the difference between client-side and server-side JavaScript

---

## 1. Node.js Architecture

### What is Node.js?
Node.js is a JavaScript runtime environment built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript on the server-side, outside of a web browser.

### Key Characteristics
- **Event-Driven**: Uses an event loop to handle asynchronous operations
- **Non-blocking I/O**: Operations don't block the execution thread
- **Single-threaded**: Uses a single main thread with event loop
- **Cross-platform**: Runs on Windows, macOS, and Linux

### V8 Engine
- Google's open-source JavaScript engine
- Compiles JavaScript to machine code
- Provides the runtime environment for JavaScript execution

### Event Loop
The event loop is the core of Node.js architecture:
1. **Call Stack**: Executes synchronous code
2. **Callback Queue**: Holds callbacks from completed async operations
3. **Event Loop**: Moves callbacks from queue to stack when stack is empty

```javascript
// Example of asynchronous execution
console.log('Start');

setTimeout(() => {
    console.log('Timeout callback');
}, 0);

console.log('End');

// Output:
// Start
// End
// Timeout callback
```

### Libuv
- C++ library that provides the event loop
- Handles file system operations, networking, and threading
- Enables cross-platform asynchronous I/O

---

## 2. NPM and Package Management

### What is NPM?
NPM (Node Package Manager) is the default package manager for Node.js that allows you to:
- Install and manage third-party libraries
- Manage project dependencies
- Run scripts and automation tasks
- Publish your own packages

### Package.json
The `package.json` file is the heart of any Node.js project:

```json
{
  "name": "my-node-app",
  "version": "1.0.0",
  "description": "A sample Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.3"
  },
  "devDependencies": {
    "nodemon": "^2.0.22",
    "jest": "^29.5.0"
  }
}
```

### Common NPM Commands

#### Initialization
```bash
npm init                    # Create package.json interactively
npm init -y                 # Create package.json with defaults
```

#### Installing Packages
```bash
npm install <package-name>          # Install and add to dependencies
npm install <package-name> --save-dev  # Install as dev dependency
npm install -g <package-name>       # Install globally
npm install                         # Install all dependencies
```

#### Managing Dependencies
```bash
npm list                    # List installed packages
npm outdated               # Check for outdated packages
npm update                 # Update packages
npm uninstall <package-name>  # Remove package
```

#### Running Scripts
```bash
npm start                  # Run start script
npm run <script-name>      # Run custom script
npm test                   # Run test script
```

### Semantic Versioning
NPM uses semantic versioning (semver):
- **Major.Minor.Patch** (e.g., 1.2.3)
- `^1.2.3` - Compatible with 1.x.x (allows minor updates)
- `~1.2.3` - Compatible with 1.2.x (allows patch updates)
- `1.2.3` - Exact version

---

## 3. File System Operations

### File System Module
Node.js provides the `fs` module for file system operations:

```javascript
const fs = require('fs');
const path = require('path');
```

### Reading Files

#### Synchronous Reading
```javascript
try {
    const data = fs.readFileSync('example.txt', 'utf8');
    console.log(data);
} catch (err) {
    console.error('Error reading file:', err);
}
```

#### Asynchronous Reading (Callback)
```javascript
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log(data);
});
```

#### Asynchronous Reading (Promises)
```javascript
const fsPromises = require('fs').promises;

async function readFileAsync() {
    try {
        const data = await fsPromises.readFile('example.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error('Error reading file:', err);
    }
}
```

### Writing Files

#### Writing Text Files
```javascript
// Asynchronous write
fs.writeFile('output.txt', 'Hello World!', 'utf8', (err) => {
    if (err) {
        console.error('Error writing file:', err);
        return;
    }
    console.log('File written successfully');
});

// Synchronous write
fs.writeFileSync('output.txt', 'Hello World!', 'utf8');
```

#### Appending to Files
```javascript
fs.appendFile('log.txt', 'New log entry\n', (err) => {
    if (err) {
        console.error('Error appending to file:', err);
        return;
    }
    console.log('Data appended successfully');
});
```

### Directory Operations

#### Creating Directories
```javascript
fs.mkdir('new-directory', { recursive: true }, (err) => {
    if (err) {
        console.error('Error creating directory:', err);
        return;
    }
    console.log('Directory created successfully');
});
```

#### Reading Directory Contents
```javascript
fs.readdir('./src', (err, files) => {
    if (err) {
        console.error('Error reading directory:', err);
        return;
    }
    console.log('Files in directory:', files);
});
```

#### Checking File/Directory Existence
```javascript
fs.access('example.txt', fs.constants.F_OK, (err) => {
    if (err) {
        console.log('File does not exist');
    } else {
        console.log('File exists');
    }
});
```

### Path Module
The `path` module helps with file and directory path operations:

```javascript
const path = require('path');

// Join paths
const fullPath = path.join(__dirname, 'files', 'example.txt');

// Get file extension
const ext = path.extname('example.txt'); // '.txt'

// Get filename
const filename = path.basename('/path/to/file.txt'); // 'file.txt'

// Get directory name
const dirname = path.dirname('/path/to/file.txt'); // '/path/to'
```

---

## 4. Building Basic Node.js Applications

### Hello World Server
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World!\n');
});

const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}/`);
});
```

### File Server Example
```javascript
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
    const filePath = path.join(__dirname, 'public', req.url);
    
    fs.readFile(filePath, (err, data) => {
        if (err) {
            res.writeHead(404, { 'Content-Type': 'text/plain' });
            res.end('File not found');
            return;
        }
        
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end(data);
    });
});

server.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

### Command Line Application
```javascript
// cli-app.js
const fs = require('fs');
const path = require('path');

// Get command line arguments
const args = process.argv.slice(2);
const command = args[0];
const filename = args[1];

switch (command) {
    case 'create':
        if (filename) {
            fs.writeFile(filename, '', (err) => {
                if (err) {
                    console.error('Error creating file:', err);
                } else {
                    console.log(`File ${filename} created successfully`);
                }
            });
        } else {
            console.log('Please provide a filename');
        }
        break;
    
    case 'read':
        if (filename) {
            fs.readFile(filename, 'utf8', (err, data) => {
                if (err) {
                    console.error('Error reading file:', err);
                } else {
                    console.log(data);
                }
            });
        } else {
            console.log('Please provide a filename');
        }
        break;
    
    default:
        console.log('Available commands: create, read');
}
```

Usage:
```bash
node cli-app.js create myfile.txt
node cli-app.js read myfile.txt
```

---

## 5. Environment Variables and Process

### Process Object
The `process` object provides information about the current Node.js process:

```javascript
// Command line arguments
console.log(process.argv);

// Environment variables
console.log(process.env.NODE_ENV);

// Current working directory
console.log(process.cwd());

// Process ID
console.log(process.pid);

// Exit the process
process.exit(0);
```

### Environment Variables
```javascript
// Set environment variables
process.env.NODE_ENV = 'development';
process.env.PORT = '3000';

// Using dotenv package for .env files
require('dotenv').config();

const port = process.env.PORT || 3000;
const dbUrl = process.env.DATABASE_URL || 'mongodb://localhost:27017/myapp';
```

---

## 6. Error Handling

### Try-Catch for Synchronous Code
```javascript
try {
    const data = fs.readFileSync('nonexistent.txt', 'utf8');
    console.log(data);
} catch (error) {
    console.error('Error:', error.message);
}
```

### Error-First Callbacks
```javascript
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error:', err.message);
        return;
    }
    console.log(data);
});
```

### Global Error Handling
```javascript
// Uncaught exceptions
process.on('uncaughtException', (error) => {
    console.error('Uncaught Exception:', error);
    process.exit(1);
});

// Unhandled promise rejections
process.on('unhandledRejection', (reason, promise) => {
    console.error('Unhandled Rejection at:', promise, 'reason:', reason);
});
```

---

## 7. Common Node.js Modules

### Built-in Modules
- `fs` - File system operations
- `http` - HTTP server and client
- `path` - File path utilities
- `url` - URL parsing
- `querystring` - Query string utilities
- `crypto` - Cryptographic functionality
- `os` - Operating system utilities
- `util` - Utility functions

### Example: URL and Query String
```javascript
const url = require('url');
const querystring = require('querystring');

const fullUrl = 'https://example.com/path?name=john&age=25';
const parsed = url.parse(fullUrl, true);

console.log(parsed.hostname); // 'example.com'
console.log(parsed.pathname); // '/path'
console.log(parsed.query);    // { name: 'john', age: '25' }
```

---

## Tutorial 3: Building Basic Node.js Applications

### Practical Exercises

1. **File Manager CLI**
   - Create a command-line tool that can create, read, update, and delete files
   - Implement directory listing functionality

2. **Log File Analyzer**
   - Read log files and extract specific information
   - Count occurrences of different log levels

3. **Simple HTTP Server**
   - Create a server that serves static files
   - Implement basic routing

4. **Package.json Workshop**
   - Create a new project with package.json
   - Install and use various NPM packages
   - Create custom scripts

---

## Summary

This chapter covered the fundamentals of Node.js, including:
- Understanding Node.js architecture and event-driven programming
- Using NPM for package management
- Performing file system operations
- Building basic applications
- Error handling patterns
- Working with built-in modules

These concepts form the foundation for building more complex server-side applications using frameworks like Express.js in the following chapters.

---

## Next Chapter Preview
**Chapter 4: MongoDB and Database Design**
- Introduction to NoSQL databases
- MongoDB operations and queries
- Database modeling and schema design
- Integration with Node.js applications

[![琴思](IMG_QS2.webp)](https://www.instagram.com/chinshi1005/)