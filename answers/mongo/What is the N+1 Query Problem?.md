### **Avoiding N+1 Queries in MongoDB with `$lookup` (Joins) and Batch Queries**

#### **What is the N+1 Query Problem?**

The **N+1 query problem** occurs when an application executes **one main query (1)** to fetch parent records and then **N additional queries** to fetch related data for each parent record. This pattern significantly increases database load and slows down performance.

For example, consider a **users and posts** relationship:

- We first fetch **N users**.
- For each user, we fetch **their posts** separately.
- This results in **N+1 queries** (1 for users + N for their posts).

#### **How to Solve N+1 Queries in MongoDB?**

We can optimize this issue using:

1. **Joins with `$lookup`** (Aggregation).
2. **Batch queries using `$in`** (Fetching related data in one query).

---

## **1. Using `$lookup` (Aggregation Joins)**

MongoDB’s `$lookup` allows us to perform a SQL-like **JOIN** between collections to fetch related data in a **single query**.

### **Example: Users and Posts**

Let's assume we have two collections:

**`users` Collection:**

```json
[
  { "_id": 1, "name": "Alice" },
  { "_id": 2, "name": "Bob" }
]
```

**`posts` Collection:**

```json
[
  { "_id": 101, "userId": 1, "title": "Alice's first post" },
  { "_id": 102, "userId": 1, "title": "Alice's second post" },
  { "_id": 103, "userId": 2, "title": "Bob's first post" }
]
```

### **Bad Approach (N+1 Queries)**

Fetching users and their posts separately (causing N+1 problem):

```javascript
const users = await db.collection("users").find().toArray(); // 1 Query

for (const user of users) {
  user.posts = await db
    .collection("posts")
    .find({ userId: user._id })
    .toArray(); // N Queries
}

console.log(users);
```

👎 **Problem:** This executes **1 query for users + N queries for posts**, leading to poor performance.

---

### **Optimized Approach with `$lookup` (Single Query)**

We can use **MongoDB aggregation** to fetch users and their posts in a **single query**:

```javascript
const usersWithPosts = await db
  .collection("users")
  .aggregate([
    {
      $lookup: {
        from: "posts", // Collection to join
        localField: "_id", // Field in users
        foreignField: "userId", // Field in posts
        as: "posts", // Output array field
      },
    },
  ])
  .toArray();

console.log(usersWithPosts);
```

### **Output:**

```json
[
  {
    "_id": 1,
    "name": "Alice",
    "posts": [
      { "_id": 101, "userId": 1, "title": "Alice's first post" },
      { "_id": 102, "userId": 1, "title": "Alice's second post" }
    ]
  },
  {
    "_id": 2,
    "name": "Bob",
    "posts": [{ "_id": 103, "userId": 2, "title": "Bob's first post" }]
  }
]
```

✅ **Now, instead of N+1 queries, we use just ONE query!** 🚀

---

## **2. Using `$in` for Batch Queries**

Another way to reduce N+1 queries is to **fetch related data in batches** using `$in`.

### **Bad Approach (N+1 Queries)**

```javascript
const users = await db.collection("users").find().toArray();

for (const user of users) {
  user.posts = await db
    .collection("posts")
    .find({ userId: user._id })
    .toArray(); // N Queries
}
```

### **Optimized Approach with `$in` (Batch Query)**

1. First, fetch all users.
2. Extract their `_id`s.
3. Fetch all posts at once using `$in`.
4. Map posts back to users.

```javascript
const users = await db.collection("users").find().toArray();
const userIds = users.map((user) => user._id);

const posts = await db
  .collection("posts")
  .find({ userId: { $in: userIds } })
  .toArray();

const userMap = new Map();
users.forEach((user) => userMap.set(user._id, { ...user, posts: [] }));

posts.forEach((post) => userMap.get(post.userId).posts.push(post));

console.log([...userMap.values()]);
```

### **Why is this better?**

✅ **Reduced Queries:** Instead of making **N+1 queries**, we now make **only 2 queries** (1 for users, 1 for posts).  
✅ **Less Latency:** Since fewer queries are executed, the response time is faster.

---

## **When to Use `$lookup` vs `$in`?**

| Approach                     | When to Use                                                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| `$lookup` (Aggregation Join) | Best for deep relationships and when you need a **single query** response.                      |
| `$in` (Batch Query)          | Best when you need more control over processing and want to fetch in **two optimized queries**. |

---

### **Summary**

1. **N+1 queries slow down performance** because they make many redundant database calls.
2. **Using `$lookup` (aggregation join)** merges related data in **one query**.
3. **Using `$in` (batch queries)** minimizes database calls by fetching all related data at once.

