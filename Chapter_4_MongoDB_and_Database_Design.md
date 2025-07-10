# Chapter 4: MongoDB and Database Design
## Full Stack Website Development I - Lecture Notes

### Course Information
- **Course Code:** FSWD101
- **Instructor:** YAB Datuk Seri Utama Prof. Dr. Lim Zhi Wei
- **Organization:** Smol Tako

---

## Learning Objectives

By the end of this chapter, students will be able to:
- Understand NoSQL database concepts and their advantages
- Install and configure MongoDB
- Perform basic and advanced MongoDB operations
- Design effective database schemas for web applications
- Implement data relationships in MongoDB
- Apply best practices for database modeling

---

## 1. Introduction to NoSQL Databases

### What is NoSQL?
NoSQL (Not Only SQL) databases are non-relational databases designed to handle large volumes of unstructured or semi-structured data. Unlike traditional relational databases, NoSQL databases don't use tables with fixed schemas.

### Types of NoSQL Databases
1. **Document Databases** (e.g., MongoDB, CouchDB)
2. **Key-Value Stores** (e.g., Redis, DynamoDB)
3. **Column-Family** (e.g., Cassandra, HBase)
4. **Graph Databases** (e.g., Neo4j, Amazon Neptune)

### Advantages of NoSQL
- **Scalability**: Easy horizontal scaling
- **Flexibility**: Dynamic schema adaptation
- **Performance**: Optimized for specific use cases
- **Cost-Effective**: Often runs on commodity hardware
- **Developer-Friendly**: JSON-like data structures

### When to Use NoSQL
- Rapid application development
- Large amounts of unstructured data
- Need for horizontal scaling
- Agile development environments
- Real-time applications

---

## 2. MongoDB Overview

### What is MongoDB?
MongoDB is a cross-platform, document-oriented NoSQL database that stores data in flexible, JSON-like documents called BSON (Binary JSON).

### Key Features
- **Document-Oriented**: Data stored in flexible documents
- **Schema-Less**: No predefined schema required
- **Indexing**: Comprehensive indexing support
- **Replication**: Built-in replication for high availability
- **Sharding**: Horizontal scaling across multiple servers
- **Aggregation**: Powerful data processing and analysis

### MongoDB vs. Relational Databases

| MongoDB | Relational Database |
|---------|-------------------|
| Document | Row |
| Collection | Table |
| Field | Column |
| Embedded Document | Join |
| Index | Index |

---

## 3. MongoDB Installation and Setup

### Installation Options
1. **MongoDB Community Server** (Local installation)
2. **MongoDB Atlas** (Cloud-based)
3. **Docker** (Containerized)

### Basic Configuration
```bash
# Start MongoDB service
sudo systemctl start mongod

# Enable MongoDB to start on boot
sudo systemctl enable mongod

# Check MongoDB status
sudo systemctl status mongod
```

### MongoDB Compass
A GUI tool for MongoDB that provides:
- Visual query builder
- Real-time performance metrics
- Schema visualization
- Index management

---

## 4. MongoDB Operations

### Basic Operations (CRUD)

#### Connect to MongoDB
```javascript
// Using MongoDB shell
mongo

// Using Node.js with MongoDB driver
const { MongoClient } = require('mongodb');
const client = new MongoClient('mongodb://localhost:27017');
```

#### Create Operations
```javascript
// Insert one document
db.users.insertOne({
  name: "John Doe",
  email: "john@example.com",
  age: 30,
  interests: ["coding", "music"]
});

// Insert multiple documents
db.users.insertMany([
  { name: "Jane Smith", email: "jane@example.com", age: 25 },
  { name: "Bob Johnson", email: "bob@example.com", age: 35 }
]);
```

#### Read Operations
```javascript
// Find all documents
db.users.find();

// Find with conditions
db.users.find({ age: { $gte: 25 } });

// Find one document
db.users.findOne({ email: "john@example.com" });

// Projection (select specific fields)
db.users.find({}, { name: 1, email: 1, _id: 0 });
```

#### Update Operations
```javascript
// Update one document
db.users.updateOne(
  { email: "john@example.com" },
  { $set: { age: 31 } }
);

// Update multiple documents
db.users.updateMany(
  { age: { $lt: 30 } },
  { $set: { category: "young" } }
);

// Replace entire document
db.users.replaceOne(
  { email: "john@example.com" },
  { name: "John Doe", email: "john@example.com", age: 31 }
);
```

#### Delete Operations
```javascript
// Delete one document
db.users.deleteOne({ email: "john@example.com" });

// Delete multiple documents
db.users.deleteMany({ age: { $lt: 18 } });
```

### Query Operators

#### Comparison Operators
```javascript
// Equal
db.users.find({ age: 30 });

// Not equal
db.users.find({ age: { $ne: 30 } });

// Greater than
db.users.find({ age: { $gt: 25 } });

// Less than or equal
db.users.find({ age: { $lte: 35 } });

// In array
db.users.find({ age: { $in: [25, 30, 35] } });
```

#### Logical Operators
```javascript
// AND
db.users.find({ $and: [{ age: { $gte: 25 } }, { age: { $lte: 35 } }] });

// OR
db.users.find({ $or: [{ age: { $lt: 25 } }, { age: { $gt: 35 } }] });

// NOT
db.users.find({ age: { $not: { $gte: 30 } } });
```

#### Array Operators
```javascript
// Array contains element
db.users.find({ interests: "coding" });

// Array contains all elements
db.users.find({ interests: { $all: ["coding", "music"] } });

// Array size
db.users.find({ interests: { $size: 2 } });
```

---

## 5. Database Modeling in MongoDB

### Schema Design Principles

#### 1. Embed vs. Reference
**Embedding** (Denormalization)
```javascript
// User with embedded address
{
  _id: ObjectId("..."),
  name: "John Doe",
  email: "john@example.com",
  address: {
    street: "123 Main St",
    city: "New York",
    zipCode: "10001"
  }
}
```

**Referencing** (Normalization)
```javascript
// User document
{
  _id: ObjectId("..."),
  name: "John Doe",
  email: "john@example.com",
  addressId: ObjectId("address_id")
}

// Address document
{
  _id: ObjectId("address_id"),
  street: "123 Main St",
  city: "New York",
  zipCode: "10001"
}
```

#### 2. When to Embed
- Small, finite data sets
- Data that doesn't change frequently
- Data that's always accessed together
- One-to-one relationships

#### 3. When to Reference
- Large data sets
- Data that changes frequently
- Many-to-many relationships
- Data that's accessed independently

### Common Schema Patterns

#### 1. One-to-One (Embedded)
```javascript
// User profile
{
  _id: ObjectId("..."),
  username: "johndoe",
  email: "john@example.com",
  profile: {
    firstName: "John",
    lastName: "Doe",
    bio: "Software developer",
    avatar: "avatar.jpg"
  }
}
```

#### 2. One-to-Many (Embedded Array)
```javascript
// Blog post with comments
{
  _id: ObjectId("..."),
  title: "MongoDB Tutorial",
  content: "...",
  comments: [
    {
      author: "Alice",
      text: "Great post!",
      date: ISODate("2024-01-15")
    },
    {
      author: "Bob",
      text: "Very helpful",
      date: ISODate("2024-01-16")
    }
  ]
}
```

#### 3. Many-to-Many (Referenced)
```javascript
// User document
{
  _id: ObjectId("user1"),
  name: "John Doe",
  email: "john@example.com"
}

// Course document
{
  _id: ObjectId("course1"),
  title: "MongoDB Basics",
  description: "Learn MongoDB fundamentals",
  enrolledUsers: [ObjectId("user1"), ObjectId("user2")]
}
```

### Data Validation
```javascript
// Schema validation
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email"],
      properties: {
        name: {
          bsonType: "string",
          description: "must be a string and is required"
        },
        email: {
          bsonType: "string",
          pattern: "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$",
          description: "must be a valid email address"
        },
        age: {
          bsonType: "int",
          minimum: 0,
          maximum: 120,
          description: "must be an integer between 0 and 120"
        }
      }
    }
  }
});
```

---

## 6. Indexes in MongoDB

### Why Indexes?
- Improve query performance
- Reduce query execution time
- Enable efficient sorting

### Types of Indexes
1. **Single Field Index**
2. **Compound Index**
3. **Multikey Index**
4. **Text Index**
5. **Geospatial Index**

### Creating Indexes
```javascript
// Single field index
db.users.createIndex({ email: 1 });

// Compound index
db.users.createIndex({ age: 1, name: 1 });

// Text index for search
db.posts.createIndex({ title: "text", content: "text" });

// Unique index
db.users.createIndex({ email: 1 }, { unique: true });
```

### Index Management
```javascript
// List all indexes
db.users.getIndexes();

// Drop index
db.users.dropIndex({ email: 1 });

// Check index usage
db.users.explain("executionStats").find({ email: "john@example.com" });
```

---

## 7. Aggregation Framework

### Pipeline Stages
```javascript
// Example: Group users by age and count
db.users.aggregate([
  {
    $group: {
      _id: "$age",
      count: { $sum: 1 },
      avgAge: { $avg: "$age" }
    }
  },
  {
    $sort: { count: -1 }
  },
  {
    $limit: 10
  }
]);
```

### Common Pipeline Operators
- `$match`: Filter documents
- `$group`: Group documents
- `$sort`: Sort documents
- `$limit`: Limit results
- `$skip`: Skip documents
- `$project`: Select fields
- `$lookup`: Join collections

---

## 8. Best Practices

### Schema Design
1. **Design for your application's queries**
2. **Favor embedding over referencing when possible**
3. **Use meaningful field names**
4. **Consider document size limitations (16MB)**
5. **Plan for data growth**

### Performance Optimization
1. **Create appropriate indexes**
2. **Use projection to limit returned fields**
3. **Implement pagination for large result sets**
4. **Monitor query performance**
5. **Use aggregation pipelines efficiently**

### Security Considerations
1. **Enable authentication**
2. **Use role-based access control**
3. **Encrypt sensitive data**
4. **Validate input data**
5. **Regular security updates**

---

## 9. Common Pitfalls to Avoid

1. **Over-embedding**: Documents become too large
2. **Under-indexing**: Queries become slow
3. **Over-indexing**: Impacts write performance
4. **Ignoring atomicity**: Not considering transaction boundaries
5. **Poor naming conventions**: Inconsistent field names

---

## 10. Practical Examples

### E-commerce Schema Design
```javascript
// Product document
{
  _id: ObjectId("..."),
  name: "Laptop",
  description: "High-performance laptop",
  price: 999.99,
  category: "Electronics",
  specifications: {
    cpu: "Intel i7",
    ram: "16GB",
    storage: "512GB SSD"
  },
  reviews: [
    {
      userId: ObjectId("..."),
      rating: 5,
      comment: "Excellent product",
      date: ISODate("2024-01-15")
    }
  ],
  inventory: {
    quantity: 50,
    warehouse: "WH001"
  }
}
```

### Blog Application Schema
```javascript
// User document
{
  _id: ObjectId("..."),
  username: "blogger123",
  email: "blogger@example.com",
  passwordHash: "...",
  profile: {
    displayName: "John Blogger",
    bio: "Tech enthusiast",
    avatar: "avatar.jpg"
  },
  createdAt: ISODate("2024-01-01")
}

// Blog post document
{
  _id: ObjectId("..."),
  title: "Getting Started with MongoDB",
  slug: "getting-started-mongodb",
  content: "...",
  author: ObjectId("user_id"),
  tags: ["mongodb", "database", "tutorial"],
  publishedAt: ISODate("2024-01-15"),
  updatedAt: ISODate("2024-01-16"),
  status: "published",
  commentCount: 5
}
```

---

## Summary

This chapter covered the fundamentals of MongoDB and database design principles. Key takeaways include:

1. Understanding NoSQL concepts and MongoDB's document-oriented approach
2. Mastering CRUD operations and query techniques
3. Learning effective schema design patterns
4. Implementing proper indexing strategies
5. Following best practices for performance and security

The knowledge gained in this chapter forms the foundation for building robust backend APIs in the following chapters of the course.