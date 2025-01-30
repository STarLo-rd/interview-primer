### **1. Data Integrity**

**Data integrity** refers to the accuracy, completeness, and consistency of data throughout its lifecycle. It ensures that data is stored and retrieved accurately without corruption, tampering, or unauthorized changes. Maintaining data integrity is essential for ensuring that the data is trustworthy and reliable for making decisions.

#### **Types of Data Integrity:**

- **Physical Integrity**: Protects data from physical damage or loss (e.g., disk failure).
- **Logical Integrity**: Ensures that the data is accurate, consistent, and meets predefined rules (e.g., data type constraints, business rules).

#### **Example of Data Integrity Violations:**

- **Corrupted Data**: Due to a hardware failure, the data stored in a database is corrupted.
- **Unauthorized Changes**: A user modifies a record that shouldn't be editable.

#### **How to Ensure Data Integrity?**

- **Validation rules**: Ensure data meets predefined conditions before insertion (e.g., range checks, format checks).
- **Encryption**: Protect sensitive data from unauthorized access.
- **Backups**: Regular backups to protect against loss.

---

### **2. Data Consistency**

**Data consistency** refers to the correctness and uniformity of data across different systems or within the same system, particularly when multiple transactions or users are involved. It ensures that the data adheres to certain business rules and that there are no conflicting or contradictory data values.

In the context of databases, consistency is part of the **ACID** (Atomicity, Consistency, Isolation, Durability) properties, which guarantee that database transactions are processed reliably.

#### **Example of Data Consistency:**

If a bank transfers money between accounts, data consistency ensures that the transfer is handled correctly, and the total balance remains consistent across both the source and destination accounts.

- **Inconsistent**: If $100 is deducted from the sender’s account but not credited to the recipient’s account, the data is inconsistent.
- **Consistent**: After a successful transfer, both the sender’s and recipient’s accounts reflect the correct balances.

#### **Consistency in Distributed Systems**:

- **CAP Theorem**: In distributed systems, consistency means that all nodes or replicas see the same data at the same time. However, maintaining strict consistency can sometimes come at the cost of availability or partition tolerance.

---

### **3. Referential Integrity**

**Referential integrity** is a concept from relational database design that ensures the relationships between tables remain consistent. Specifically, it ensures that **foreign key values in one table must match primary key values in another table**, or that they must be **null**.

Referential integrity is crucial for preventing **orphaned records** or invalid relationships between tables. It enforces the **correctness of relationships** and ensures that data remains valid across the database.

#### **Example of Referential Integrity:**

Consider two tables in a database:

- **`orders`** (with columns: `order_id`, `customer_id`)
- **`customers`** (with columns: `customer_id`, `name`)

If an order is placed by a customer, the `customer_id` in the `orders` table should always refer to a valid `customer_id` in the `customers` table. If a customer is deleted from the `customers` table, the system should prevent any orders that refer to that deleted `customer_id`, or it should automatically handle those references (e.g., by setting them to null).

#### **Referential Integrity Rules**:

- **Foreign Key Constraints**: Ensure that every foreign key in a table corresponds to a primary key in another table.
- **Delete Cascade**: If a parent record is deleted, related child records should also be deleted automatically (or set to `null`).
- **Update Cascade**: If a primary key value is updated, the corresponding foreign key values in related tables are updated as well.

#### **Example in SQL:**

```sql
CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  customer_id INT,
  FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

In this example, the `orders` table cannot contain a `customer_id` that does not exist in the `customers` table, preserving referential integrity.

---

### **Summary of Key Concepts:**

1. **Data Integrity**: Ensures that data remains accurate, consistent, and free from corruption throughout its lifecycle.

   - **Types**: Physical (protection from hardware failures) and logical (ensuring data meets predefined rules).

2. **Data Consistency**: Ensures that data follows predefined rules and is uniform across all systems. It's part of the **ACID** properties, ensuring that data remains correct during transactions.

3. **Referential Integrity**: Ensures that foreign key values in a relational database match primary key values in another table, maintaining valid relationships between tables.

---

Would you like to dive deeper into any of these concepts, or see examples in code?
