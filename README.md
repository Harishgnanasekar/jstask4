#  INTERMEDIATE LEVEL – FUNCTIONS

## SECTION 1: Real-Time Function Logic

---

## 1️⃣ Payroll System

### **Function Code**

```js
function calculateSalary(basicSalary, bonusPercentage) {
  const bonus = (basicSalary * bonusPercentage) / 100;
  const salaryWithBonus = basicSalary + bonus;
  const tax = salaryWithBonus * 0.05;
  const finalSalary = salaryWithBonus - tax;

  return {
    basicSalary,
    bonus,
    tax,
    finalSalary
  };
}
```

### **Example Usage**

```js
console.log(calculateSalary(20000, 10));
```

### **Explanation**

* Bonus is calculated using percentage
* 5% tax deducted from salary + bonus
* Final salary returned as an object

---

## 2️⃣ Student Result System

### **Function Code**

```js
function generateResult(name, marksArray) {
  const total = marksArray.reduce((sum, mark) => sum + mark, 0);
  const average = total / marksArray.length;

  let grade;
  if (average >= 80) grade = "A";
  else if (average >= 60) grade = "B";
  else grade = "Fail";

  return {
    name,
    total,
    average,
    grade
  };
}
```

### **Example Usage**

```js
console.log(generateResult("Harish", [70, 80, 75]));
```

### **Explanation**

* Calculates total & average
* Decides grade based on average
* Returns a result object

---

#  SECTION 2: Scope & Hoisting (Debugging)

---

## 3️⃣ Debug This Code

### **Given Code**

```js
function demo() {
  if (true) {
    var a = 10;
    let b = 20;
  }

  console.log(a);
  console.log(b);
}
```

### ❓ What will happen?

* `a` prints **10**
* `b` throws **ReferenceError**

### ❓ Why?

* `var` is **function scoped**
* `let` is **block scoped**

###  Fixed Code

```js
function demo() {
  let a, b;
  if (true) {
    a = 10;
    b = 20;
  }
  console.log(a);
  console.log(b);
}
```

---

## 4️⃣ Hoisting Analysis

### **Code**

```js
console.log(x);
var x = 100;

console.log(y);
let y = 200;
```

### 🔍 Output

```
undefined
ReferenceError
```

### 📘 Explanation

* `var x` is hoisted → initialized as `undefined`
* `let y` is hoisted but **not initialized** → Temporal Dead Zone

---

#  SECTION 3: Callback & Higher Order Functions

---

## 5️⃣ Order Processing System

### **Function Code**

```js
function processOrder(orderId, callback) {
  console.log("Order Processed");
  callback(orderId);
}

function generateInvoice(orderId) {
  console.log("Invoice generated for order:", orderId);
}
```

### **Usage**

```js
processOrder(101, generateInvoice);
```

---

## 6️⃣ Bank Transaction System

### **Function Code**

```js
function transaction(amount, type, callback) {
  let balance = 1000;

  if (type === "deposit") {
    balance += amount;
  } else if (type === "withdraw") {
    balance -= amount;
  }

  callback(balance);
}

function sendSMS(balance) {
  console.log("SMS Sent. Current Balance:", balance);
}
```

### **Usage**

```js
transaction(500, "deposit", sendSMS);
```

---

#  SECTION 4: Currying (E-Commerce)

---

## 7️⃣ Dynamic Price Builder

### **Function Code**

```js
function priceBuilder(basePrice) {
  return function (discount) {
    return function (tax) {
      const discountAmount = basePrice * (discount / 100);
      const priceAfterDiscount = basePrice - discountAmount;
      const taxAmount = priceAfterDiscount * (tax / 100);
      return priceAfterDiscount + taxAmount;
    };
  };
}
```

### **Example**

```js
console.log(priceBuilder(2000)(15)(18));
```

### **Explanation**

* Applies discount first
* Then applies tax
* Returns final price using currying

---

#  SECTION 5 – IIFE (Security + Encapsulation)

## 8️⃣ Secure Company Module

### **Requirement**

* Store private variable `companyCode`
* Expose `getCompanyStatus()`
* `companyCode` must NOT be directly accessible

###  **Correct Answer (Using IIFE)**

```js
const CompanyModule = (function () {
  const companyCode = "CMP2025"; // private variable

  function getCompanyStatus() {
    return "Company Active - Code Verified";
  }

  return {
    getCompanyStatus
  };
})();
```

### **Usage**

```js
console.log(CompanyModule.getCompanyStatus());
```

### **Explanation**

* `companyCode` is hidden inside IIFE
* Only public method is exposed
* Provides security & encapsulation

---

#  SECTION 6 – Generator (Advanced Logic)

---

## 9️⃣ Unique Order ID Generator

### **Requirement**

Generate: `ORD1001`, `ORD1002`, `ORD1003`, …

###  **Correct Answer**

```js
function* orderIdGenerator() {
  let id = 1001;
  while (true) {
    yield `ORD${id}`;
    id++;
  }
}
```

### **Usage**

```js
const gen = orderIdGenerator();
console.log(gen.next().value);
console.log(gen.next().value);
console.log(gen.next().value);
```

### **Output**

```
ORD1001
ORD1002
ORD1003
```

---

## 🔟 Coupon Spin System

### **Requirement**

Yield:

* 10% OFF
* 20% OFF
* 50% OFF
* No Luck
* Jackpot
  Simulate multiple spins

###  **Correct Answer**

```js
function* couponGenerator() {
  const coupons = [
    "10% OFF",
    "20% OFF",
    "50% OFF",
    "No Luck",
    "Jackpot"
  ];

  while (true) {
    const randomIndex = Math.floor(Math.random() * coupons.length);
    yield coupons[randomIndex];
  }
}
```

### **Usage**

```js
const spin = couponGenerator();
console.log(spin.next().value);
console.log(spin.next().value);
console.log(spin.next().value);
```

---

#  SECTION 7 – Mini Project (Integrated)

## 🛒 Mini E-Commerce Flow

---

### 1️⃣ addToCart(product, price)

```js
let cart = [];

function addToCart(product, price) {
  cart.push({ product, price });
}
```

---

### 2️⃣ calculateTotal()

```js
function calculateTotal() {
  return cart.reduce((sum, item) => sum + item.price, 0);
}
```

---

### 3️⃣ applyDiscount() – Using Currying

```js
function applyDiscount(discount) {
  return function (total) {
    return total - (total * discount) / 100;
  };
}
```

---

### 4️⃣ generateCoupon() – Using Generator

```js
function* generateCoupon() {
  yield "10% OFF";
  yield "20% OFF";
  yield "50% OFF";
}
```

---

### 5️⃣ processPayment() – Using Callback

```js
function processPayment(amount, callback) {
  console.log("Processing payment of ₹", amount);
  callback();
}

function paymentSuccess() {
  console.log("Payment Successful");
}
```

---

### 6️⃣ Hide Config Using IIFE

```js
const config = (function () {
  const apiKey = "SECRET123";
  return {
    getKey: () => "Access Granted"
  };
})();
```

---

#  CONCEPT QUESTIONS

---

## 1️⃣ Difference between Function Declaration & Expression

| Function Declaration            | Function Expression                |
| ------------------------------- | ---------------------------------- |
| Hoisted                         | Not hoisted                        |
| Can be called before definition | Cannot be called before definition |

```js
function test() {}      // Declaration
const demo = function() {}; // Expression
```

---

## 2️⃣ What is Higher Order Function?

A function that:

* Accepts another function as argument OR
* Returns a function

### Example:

```js
function higherOrder(fn) {
  fn();
}
```

---

## 3️⃣ Real-Time Example of Generator

✔ Pagination
✔ Order ID generation
✔ Coupon spin system
✔ Infinite scrolling data

---

## 4️⃣ Why do we use IIFE?

* Avoid global scope pollution
* Data privacy
* Encapsulation
* Secure variables

---

## 5️⃣ Difference between `var`, `let`, `const`

| Feature  | var      | let   | const |
| -------- | -------- | ----- | ----- |
| Scope    | Function | Block | Block |
| Hoisting | Yes      | TDZ   | TDZ   |
| Reassign | Yes      | Yes   | ❌ No  |

---



