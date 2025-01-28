### **Core Principles of Schema Design**

1. **Understand the Requirements**:

   - Identify the core entities (e.g., Users, Orders, Products).
   - Understand relationships between entities (one-to-one, one-to-many, many-to-many).
   - Map functional requirements to data models.

   > **Note** Start with the requirements at first, if the interview just gives you the problem statement, don't start/design/create model/coding, discuss with him, understand the problem and get the requirement first then analyse the entity to get started

2. **Normalize Your Schema**:

   - Eliminate redundancy by breaking data into smaller tables or collections.
   - Avoid over-normalization if it impacts performance. Strike a balance.

3. **Think of Query Patterns**:

   - Anticipate how the data will be read and written.
   - Optimize the schema for the most frequent queries.

4. **Plan for Growth**:
   - Design with scalability in mind (e.g., sharding, indexing, denormalization for reads).

---

### **Practical Exercise: Schema Design Examples**

#### Example 1: Blog Platform

**Requirements**:

1. Users can write posts.
2. Posts can have multiple comments.
3. Posts can belong to one or more categories.

**Schema**:

- **User**: `{ userId, name, email, bio }`
- **Post**: `{ postId, userId, title, content, createdAt, categories: [categoryId] }`
- **Comment**: `{ commentId, postId, userId, content, createdAt }`
- **Category**: `{ categoryId, name }`

---

#### Example 2: Online Food Delivery

**Requirements**:

1. Customers can place multiple orders.
2. An order can have multiple items.
3. Each item belongs to a menu.

**Schema**:

- **Customer**: `{ customerId, name, email, address }`
- **Order**: `{ orderId, customerId, orderDate, totalAmount }`
- **OrderItem**: `{ itemId, orderId, menuItemId, quantity, price }`
- **MenuItem**: `{ menuItemId, name, price, category }`

---

### **Exercises for You**

1. **E-Commerce Example**:
   Design a schema for an e-commerce platform where:

   - Customers can add products to a cart.
   - Orders track customer information, products, and order status.
   - Products have stock levels.

2. **Social Media Example**:
   Design a schema for a social media app where:

   - Users can follow other users.
   - Users can post images with captions.
   - Posts can have likes and comments.

3. **Movie Booking System**:
   Design a schema for a movie ticket booking system where:
   - Movies have showtimes and theaters.
   - Users can book multiple seats for a show.
   - Theaters have seat availability.

---

## Solutions

### E-Commerce Example

**Schema**:

- **Customer**: `{ customerId, name, email (unique, indexed), address, cartId }`
- **Order**: `{ orderId, customerId, orderDate, status, totalAmount, products: [{ productId, quantity, price }] }`
- **Cart**: `{ cartId, customerId, products: [{ productId, quantity }], totalAmount }`
- **Product**: `{ productId, productName, price, stock, description, category }`

---

### **Refined E-Commerce Schema**

#### **1. Customers**

```json
{
  "customerId": "string (unique)",
  "name": "string",
  "email": "string (unique, indexed)",
  "address": "string",
  "cartId": "string (reference to Carts)"
}
```

- **Why**:
  - `email` should be indexed since it's commonly used for logins or lookups.
  - `cartId` links the customer to their cart.

---

#### **2. Carts**

```json
{
  "cartId": "string (unique)",
  "customerId": "string (reference to Customers)",
  "products": [
    {
      "productId": "string (reference to Products)",
      "quantity": "number"
    }
  ],
  "totalAmount": "number"
}
```

- **Why**:
  - Added `quantity` for products in the cart.
  - Added `totalAmount` for calculating the cart's value efficiently without recalculating every time.

---

#### **3. Orders**

```json
{
  "orderId": "string (unique)",
  "customerId": "string (reference to Customers)",
  "orderDate": "Date",
  "status": "string (enum: pending, shipped, delivered, cancelled)",
  "totalAmount": "number",
  "products": [
    {
      "productId": "string (reference to Products)",
      "quantity": "number",
      "price": "number (at the time of purchase)"
    }
  ]
}
```

- **Why**:
  - Added `status` to track the order lifecycle.
  - Each product in the `products` array includes `price` to avoid issues if the product's price changes after the order is placed.

---

#### **4. Products**

```json
{
  "productId": "string (unique)",
  "productName": "string",
  "price": "number",
  "stock": "number",
  "description": "string",
  "category": "string"
}
```

- **Why**:
  - Added `stock` to track inventory levels.
  - Added `description` and `category` for better product metadata.

---

### **Relationships**

1. **Customers → Carts**:

   - One-to-One: A customer can have only one cart at a time.

2. **Carts → Products**:

   - Many-to-Many: A cart can contain multiple products, and a product can be in multiple carts.

3. **Orders → Products**:
   - Many-to-Many: An order can contain multiple products, and each product can be part of multiple orders.

---

### **Schema Design Considerations**

1. **Denormalization in Orders**:

   - Storing `price` at the time of purchase ensures data consistency if product prices change.

2. **Indexing**:

   - Use indexes for frequently queried fields like `email` in Customers, `productId` in Products, and `orderId` in Orders.

3. **Scalability**:

   - Ensure `Products` collection is optimized for heavy reads (e.g., product listing).
   - Handle `Orders` carefully as it grows rapidly.

4. **Concurrency**:
   - Implement locking or transactions to handle cases like multiple customers adding the same product to their cart.

---

Your schema is a good starting point, but here's a refined and more comprehensive version:

---

### **Schema**:

    Users: { userId, name, email (unique, indexed), bio, profilePicUrl, followers: [userIds], following: [userIds] }
    Posts: { postId, userId (reference to Users), title, description, imageUrl, likes: [userIds], comments: [commentIds], createdAt }
    Comments: { commentId, userId (reference to Users), postId (reference to Posts), description, createdAt }

---

### Relationships:

1. **Users → Posts**:

   - One-to-Many: A user can create multiple posts.

2. **Users → Users**:

   - Many-to-Many: Users can follow/unfollow other users.

3. **Posts → Comments**:

   - One-to-Many: A post can have multiple comments.

4. **Posts → Users (Likes)**:
   - Many-to-Many: A post can be liked by multiple users, and a user can like multiple posts.

---
