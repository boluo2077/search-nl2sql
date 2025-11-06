<a id="top"></a>

<div align="center">

# [🔍 Search NL2SQL: Bringing Data Queries Back to Basics](https://github.com/boluo2077/search-nl2sql)

**[ English | [中文](README.zh-CN.md) ]**

</div>

---

### 🤔 What is Search NL2SQL?

Imagine this: when you're shopping on Amazon, would you type "Please help me find blue dresses in the product database with prices between $15 and $30"? Of course not! You'd simply type: **"blue dress $15-$30"**

**Search NL2SQL** brings this intuitive search mindset to database queries. It lets users query databases just like using a search engine—**type keywords, the system understands intelligently**

---

## 📊 The Fundamental Difference Between Two Approaches

### 🔹 Traditional NL2SQL System Prompt Example

```markdown
- Current time: Tuesday, November 11, 2025, 11:11:11 AM

## Table Structure and Data Types

Table: Products
product_id: VARCHAR (Product ID)
product_name: VARCHAR (Product Name)
product_price: DECIMAL (Product Price)
product_stock: INT (Product Stock)
product_launch_date: DATETIME (Product Launch Date)

Table: Customers
customer_id: VARCHAR (Customer ID)
customer_name: VARCHAR (Customer Name)
customer_phone: VARCHAR (Customer Phone)
customer_address: VARCHAR (Customer Address)
customer_registration_date: DATETIME (Customer Registration Date)

Table: Orders
order_id: VARCHAR (Order ID)
customer_id: VARCHAR (Customer ID)
customer_name: VARCHAR (Customer Name)
order_amount: DECIMAL (Order Amount)
order_address: VARCHAR (Order Address)
order_creation_date: DATETIME (Order Creation Date)
```

**Characteristics**: Provides abstract table structure definitions; AI needs to understand field types and relationships

---

### 🔹 Search NL2SQL System Prompt Example

```markdown
- Current time: Tuesday, November 11, 2025, 11:11:11 AM
- Infer fields from the data samples, then infer tables from the fields
- Before using the SQL code interpreter tool, explain your inference approach
- If multiple SQL queries are possible, present options for the user to choose

## Table Structure with Data Examples

Table: Products
product_id: p-985
product_name: QB826G Power Bank (Product Name)
product_price: 200 (Product Price)
product_stock: 100 (Product Stock)
product_launch_date: 2025-09-03 09:00:00 (Product Launch Date)

Table: Customers
customer_id: c-99
customer_name: John Smith (Customer Name)
customer_phone: 13812345678 (Customer Phone)
customer_address: No.2 YY Road, Haidian District, Beijing, China (Customer Address)
customer_registration_date: 2025-10-01 10:00:00 (Customer Registration Date)

Table: Orders
order_id: o-8848
customer_id: c-66
customer_name: Jane Doe (Customer Name)
order_amount: 400 (Order Amount)
order_address: No.1 XX Road, Chaoyang District, Beijing, China (Order Address)
order_creation_date: 2025-11-11 11:00:00 (Order Creation Date)
```

**Characteristics**: Provides real data samples; AI understands user input by "seeing what the data looks like"

---

## 💡 Design Philosophy

### 1️⃣ **Reverse Inference**
Infer field characteristics from data samples:
- See `13812345678` → Infer it's a phone number
- See `QB826G Power Bank` → Infer it's a product name
- See `Shanghai` → Infer it's likely an address field

### 2️⃣ **Semantic Compression**
Support ultra-concise natural language expressions:
- `yesterday` → `BETWEEN '2025-06-05' AND '2025-06-06'`
- `last year` → `BETWEEN '2024-01-01' AND '2025-01-01'`
- `500-1000` → `BETWEEN 500 AND 1000`
- `>500` / `<500` → Automatically recognize comparison operators

### 3️⃣ **Intelligent Decision-Making**
When multiple interpretations exist, present choices to the user:

```
You entered: "John Smith"

I've identified the following possible query intents:
A. Find customers named "John Smith" in the Customers table
B. Find orders with customer name "John Smith" in the Orders table

Please choose: A or B?
```

---

## 🎯 Interaction Comparison: Revolutionary Efficiency Gains

> **📌 Character Count Note**:
> - All character counts below are based on **English characters**
> - **Phone numbers** are typically copy-pasted, counted as **4 characters** (the operational cost of Ctrl + C and Ctrl + V)

---

### 📱 Scenario 1: Query Single Customer Information

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find all information about the customer whose phone number is 15690374821 in the customer information table | 122 chars | - |
| **Search NL2SQL** | `15690374821` | 4 chars | **🚀 2950%** |

**Expected SQL**: `SELECT * FROM Customers WHERE customer_phone = '15690374821'`

---

### 📱 Scenario 2: Query Multiple Customers

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find all information about customers whose phone numbers are either 15690374821 or 13826548392 in our customer database | 134 chars | - |
| **Search NL2SQL** | `15690374821 13826548392` | 9 chars | **🚀 1389%** |

**Expected SQL**: `SELECT * FROM Customers WHERE customer_phone IN ('15690374821', '13826548392')`

---

### 💰 Scenario 3: Exact Amount Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find order records where the customer name is John Smith and the order amount is exactly 500 dollars | 115 chars | - |
| **Search NL2SQL** | `John Smith 500` | 14 chars | **🚀 721%** |

**Expected SQL**: `SELECT * FROM Orders WHERE customer_name = 'John Smith' AND order_amount = 500`

---

### 💰 Scenario 4: Comparison Operator Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find order records where the customer name is John Smith and the order amount is less than 500 dollars | 117 chars | - |
| **Search NL2SQL** | `John Smith <500` | 15 chars | **🚀 680%** |

**Expected SQL**: `SELECT * FROM Orders WHERE customer_name = 'John Smith' AND order_amount < 500`

---

### 🌍 Scenario 5: Fuzzy Search + Range Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find all orders where the delivery address contains Shanghai and the order amount is greater than 500 dollars | 124 chars | - |
| **Search NL2SQL** | `Shanghai >500` | 13 chars | **🚀 854%** |

**Expected SQL**: `SELECT * FROM Orders WHERE order_address LIKE '%Shanghai%' AND order_amount > 500`

---

### 🌍 Scenario 6: BETWEEN Range Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find all orders where the delivery address contains Shanghai and the order amount is between 500 and 1000 dollars | 128 chars | - |
| **Search NL2SQL** | `Shanghai 500-1000` | 17 chars | **🚀 653%** |

**Expected SQL**: `SELECT * FROM Orders WHERE order_address LIKE '%Shanghai%' AND order_amount BETWEEN 500 AND 1000`

---

### 📅 Scenario 7: Relative Time Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | Please help me find all products where the product name contains phone case and the launch date was yesterday | 109 chars | - |
| **Search NL2SQL** | `phone case yesterday` | 20 chars | **🚀 445%** |

**Expected SQL**: `SELECT * FROM Products WHERE product_name LIKE '%phone case%' AND product_launch_date BETWEEN '2025-11-10' AND '2025-11-11'`

---

### 🎯 Scenario 8: Complex Multi-Condition Query

| Method | User Input | Characters | Efficiency Gain |
|--------|-----------|-----------|-----------------|
| **Traditional NL2SQL** | I want to comprehensively query order data: please find all orders created last year that meet the following conditions: first, the delivery address must contain Shanghai; second, the customer name is either Wang Wu or Zhao Liu; third, the order amount must be greater than 500 dollars. Please list all detailed information for orders meeting these criteria | 357 chars | - |
| **Search NL2SQL** | `last year Shanghai Wang Wu Zhao Liu >500` | 40 chars | **🚀 793%** |

**Expected SQL**:
```sql
SELECT * FROM Orders
WHERE order_creation_date BETWEEN '2024-01-01' AND '2025-01-01'
  AND order_address LIKE '%Shanghai%'
  AND customer_name IN ('Wang Wu', 'Zhao Liu')
  AND order_amount > 500
```

---

## 📏 Character Count Comparison

| Scenario Type | Traditional | Search | Chars Saved | Efficiency Gain |
|--------------|------------|--------|-------------|-----------------|
| Single Phone Query | 122 | **4** | 118 | 2950% |
| Dual Phone Query | 134 | **9** | 125 | 1389% |
| Name + Exact Amount | 115 | **14** | 101 | 721% |
| Name + Comparison | 117 | **15** | 102 | 680% |
| Address + Comparison | 124 | **13** | 111 | 854% |
| Address + Range | 128 | **17** | 111 | 653% |
| Product + Time | 109 | **20** | 89 | 445% |
| Complex Multi-Condition | 357 | **40** | 317 | 793% |

---

## 🎯 Core Advantages

### ✅ **Dramatically Reduced Cognitive Load**
No need to think about "how to describe"—just type "what you know"

### ✅ **Skyrocketing Operational Efficiency**
Average input efficiency improved by **600% - 3000%**; copy-paste completes queries

### ✅ **Zero Learning Curve**
As intuitive as using Google Search—zero barrier to entry

### ✅ **Enhanced Error Tolerance**
Keyword order doesn't matter: `John Smith 500` equals `500 John Smith`

---

## 🌟 Summary

**Search NL2SQL** isn't just a technical optimization—it's a **paradigm shift in interaction**. It brings data queries from "conversation" back to "search," from "describing requirements" back to "entering keywords," letting machines understand humanity's most natural way of expression

> **The best technology is the one users don't even notice**

---

<div align="center">

**If this project helps you, please click the ⭐ Star in the top right corner!**

*Your Star is our motivation to keep improving 💪*

![Star History Chart](https://api.star-history.com/svg?repos=boluo2077/search-nl2sql&type=Date)

---

<a href="#top">
  <img src="https://img.shields.io/badge/⬆️-Back_to_Top-blue?style=for-the-badge" alt="Back to Top">
</a>

</div>
