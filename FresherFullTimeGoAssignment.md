### **Fresher Full Time Assignment: Order Management System for Stock Trading**

#### **Objective:**
Develop a simple Order Management System (OMS) that handles client orders for stock trading. The system should manage long buys, short sells, and square-off orders and maintain positions.

---

### **Prerequisites:**
- Basic understanding of stock trading concepts such as **long buy**, **short selling**, and **positions**.
- Familiarity with REST APIs and basic data structures.

---

### **Requirements:**

#### **1. System Overview:**
The Order Management System (OMS) will:
- Accept client orders via API requests.
- Update client positions based on the type of order (long buy, short sell, or square-off).
- Provide an API to fetch client positions.

---

#### **2. API Specifications:**

##### **API 1: `newOrder`**
- **Endpoint:** `/newOrder`
- **Method:** `POST`
- **Request Body:**
  ```json
  {
    "clientId": "int32",       // Unique identifier for the client
    "stockId": "int32",        // Unique identifier for the stock
    "quantity": "int32",       // Positive for long/buy, negative for short/sell
    "price": "float32"         // Price at which the order is executed
  }
  ```
- **Behavior:**
  - If the `quantity` sign (positive/negative) matches the client's existing positions for the stock:
    - Increase the total positions for that stock.
  - If the `quantity` sign is opposite to the client's existing positions:
    - Treat the order as a **square-off** and reduce positions..
  - Handle edge cases which you can think of.

---

##### **API 2: `clientDetails`**
- **Endpoint:** `/clientDetails`
- **Method:** `GET`
- **Query Parameters:**
  - `clientId`: `int32` (Unique identifier for the client)
  - `stockId`: `int32` (Unique identifier for the stock)
- **Response Body:**
  ```json
  {
    "clientId": "int32",
    "stockId": "int32",
    "positions": {
        "quantity": "int32",  // Positive for long, negative for short
        "average_entry_price": "float32",   
      }
  }
  ```

---

#### **3. Key Logic:**

1. **positions Update:**
   - For **long buy** (positive quantity):
     - Increase the client's positions for the stock in the exisitng positions are positive.
     - Decrease the client's positions for the stock in the exisitng positions are negative.

   - For **short sell** (negative quantity):
     - Increase the client's short position for the stock in the exisitng positions are also negative.
     - Decrease the client's positions for the stock in the exisitng positions are positive.

3. **Maintain Position:**
   - Maintain the holdings at all time.

---

#### **4. Example Scenarios:**

##### **Scenario 1: Net Buy Position **
- Client A bought 100 shares of Stock X at ₹ 50 (short sell). 
- positions: `{stockId: X, quantity: 100, Price: 50}`

##### **Scenario 2: Continue to have Net Buy Position**
- Client A sells 50 shares of Stock X at ₹65 (short sell).
- positions: `{stockId: X, quantity: 150, Price: 55}`

##### **Scenario 3: Square-Off**
- Client A sells 110 shares of Stock X at ₹60 (square-off).
- Reduce 110 shares from the position.
- Updated positions: `{stockId: X, quantity: 40, averagePrice: 55}`

---

#### **5. Deliverables:**
1. **Code Implementation:**
   - Implement the `newOrder` and `clientDetails` APIs.
   - Use GO as the programming language.

2. **Documentation:**
   - Provide a README file with:
     - Instructions to set up and run the system.
     - Explanation of the design and data structures used.

3. **Bonus (Optional):**
   - Add error handling for invalid inputs (e.g., negative price, invalid client/stock IDs).
   - Include unit tests for key functionalities.

---

#### **6. Evaluation Criteria:**
- **Functionality:** Correct implementation of order management and maintaining holdings.
- **Edge Case:** Figuring and handling edge cases.
- **Code Quality:** Clean, modular, and well-documented code.
- **Error Handling:** Graceful handling of edge cases and invalid inputs.
- **Testing:** Comprehensive unit tests for all key functionalities.

---

### **Notes:**
- Use `gin` router.
- Use in-memory data structures (e.g., dictionaries, lists) to store positions. A database is not required.
- Focus on simplicity and clarity while ensuring the system meets the requirements.

---
