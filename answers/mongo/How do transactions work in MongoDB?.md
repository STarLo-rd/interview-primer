### **What is a Transaction?**

A **transaction** is a logical unit of work that includes one or more operations that must all be completed successfully for the system to remain in a consistent state. Transactions are designed to ensure **data integrity** and **consistency** across multiple operations.

In a database context, a transaction typically involves the following properties, known as the **ACID properties**:

- **Atomicity**: Ensures that all operations within a transaction are treated as a single unit. Either all operations succeed, or none of them do. If one operation fails, the entire transaction is rolled back.
- **Consistency**: Ensures that the database moves from one valid state to another. Any changes made within a transaction must be in line with the rules and constraints of the database.
- **Isolation**: Ensures that operations in a transaction are isolated from the operations of other transactions. This prevents transactions from interfering with each other, even if they are running concurrently.
- **Durability**: Ensures that once a transaction has been committed, its changes are permanent, even if the system crashes.

### **Transactions in MongoDB**

In MongoDB, transactions allow you to perform multiple read and write operations across **multiple documents** or even **multiple collections** within a single operation. Transactions in MongoDB support the ACID properties, which means that MongoDB will ensure **atomicity**, **consistency**, **isolation**, and **durability** for operations within a transaction.

MongoDB introduced **multi-document transactions** in **version 4.0** (for replica sets) and expanded it to **sharded clusters** in **version 4.2**. This allows you to perform a series of operations across multiple documents and collections while ensuring that all of the changes are consistent and reliable.

---

### **How Do Transactions Work in MongoDB?**

#### **1. Starting a Transaction**

In MongoDB, you can start a transaction using the `startSession()` method, which creates a session object. The session is then passed to the various operations to make sure they belong to the same transaction.

```javascript
const session = await client.startSession();
```

You can then use this session to start and manage the transaction.

#### **2. Running Operations Inside a Transaction**

After starting a session, you can run operations (e.g., `insert`, `update`, `delete`) on documents within the scope of that session. These operations will be part of the transaction.

```javascript
const transactionOptions = {
  readConcern: { level: "majority" },
  writeConcern: { w: "majority" },
};

session.startTransaction(transactionOptions);

try {
  // Operations inside the transaction
  await db
    .collection("users")
    .updateOne({ _id: userId }, { $set: { balance: newBalance } }, { session });

  await db
    .collection("transactions")
    .insertOne(
      { userId, amount: transactionAmount, type: "debit" },
      { session }
    );

  // Commit the transaction if all operations are successful
  await session.commitTransaction();
} catch (error) {
  // If any operation fails, abort the transaction
  await session.abortTransaction();
} finally {
  // End the session
  session.endSession();
}
```

#### **3. Committing a Transaction**

After performing all necessary operations, you can commit the transaction using `session.commitTransaction()`. This will persist the changes to the database.

```javascript
await session.commitTransaction();
```

#### **4. Rolling Back a Transaction (Abort)**

If something goes wrong during the transaction, you can **abort** the transaction using `session.abortTransaction()`. This ensures that all changes made during the transaction are rolled back, maintaining the integrity of the database.

```javascript
await session.abortTransaction();
```

#### **5. Ending the Session**

After committing or aborting the transaction, the session should be ended using `session.endSession()`, which will clean up any resources related to the session.

```javascript
session.endSession();
```

---

### **Key Considerations for MongoDB Transactions**

1. **Transaction Scope**:

   - MongoDB transactions support operations across multiple **documents** and **collections** within a **single database**. However, MongoDB transactions do not span across multiple databases in a single transaction.

2. **ACID Properties**:

   - MongoDB transactions fully support **ACID properties**. The system will guarantee atomicity, consistency, isolation, and durability for the operations within a transaction.

3. **Write Concerns and Read Concerns**:

   - Transactions in MongoDB use **write concerns** and **read concerns** to ensure data consistency and durability.
     - **Write Concern** specifies the level of acknowledgment required from the database after an operation.
     - **Read Concern** specifies the consistency level of the data read during the transaction.

4. **Performance Impact**:

   - While transactions ensure data integrity, they can have a **performance overhead** compared to single-operation writes. This overhead arises from maintaining the transaction state and ensuring consistency across multiple operations.

5. **Automatic Rollback**:

   - If the application crashes or the session is not committed or aborted properly, MongoDB will automatically roll back any changes made during the transaction.

6. **Sharded Clusters**:
   - MongoDB supports multi-document transactions in **sharded clusters** (introduced in version 4.2). This allows transactions to span across multiple shards, which is important for scalability in large distributed systems.

---

### **Example Use Cases for Transactions**

1. **Banking Systems**:

   - Transactions can be used to ensure that money is transferred between accounts atomically. For example, when transferring funds from one account to another, both the debit from the sender's account and the credit to the recipient's account should either succeed together or fail together.

2. **E-Commerce Orders**:

   - When placing an order in an e-commerce system, the transaction could include operations like updating the inventory, processing the payment, and storing the order details, ensuring that all actions succeed or fail as a unit.

3. **Inventory Management**:
   - In an inventory system, updating stock levels and recording the transactions must be done together. If the stock update fails, the transaction is aborted to avoid incorrect inventory data.

---

### **MongoDB Transaction Example (Full Example)**

```javascript
const { MongoClient } = require("mongodb");

async function runTransaction() {
  const client = new MongoClient("mongodb://localhost:27017");
  const session = client.startSession();

  try {
    const transactionOptions = {
      readConcern: { level: "majority" },
      writeConcern: { w: "majority" },
    };

    session.startTransaction(transactionOptions);

    // Example of transaction operations:
    const usersCollection = client.db("shop").collection("users");
    const ordersCollection = client.db("shop").collection("orders");

    // Update user's balance
    await usersCollection.updateOne(
      { _id: "user123" },
      { $inc: { balance: -100 } },
      { session }
    );

    // Insert order
    await ordersCollection.insertOne(
      { userId: "user123", amount: 100, date: new Date() },
      { session }
    );

    // Commit the transaction if everything is successful
    await session.commitTransaction();
    console.log("Transaction committed.");
  } catch (error) {
    // If any error occurs, abort the transaction
    console.log("Transaction aborted due to an error.");
    await session.abortTransaction();
  } finally {
    session.endSession();
    await client.close();
  }
}

runTransaction().catch(console.error);
```

---

### **Conclusion**

MongoDB transactions provide a powerful way to ensure that multiple operations are executed atomically and consistently, making them crucial for applications where data integrity is important. By supporting multi-document and multi-collection transactions, MongoDB provides full ACID guarantees, ensuring the reliability of your data even in complex scenarios.
