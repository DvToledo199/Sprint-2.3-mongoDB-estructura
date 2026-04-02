# MongoDB Data Modeling – Sprint 2.3


## Exercise 1 – Optics Management (Client View)

This exercise represents a database for an optical store from the client's point of view.

### Collections

- clients  
  Stores customer information, including personal data, address and purchase history.

- glasses  
  Contains the product catalog with details such as brand, graduation, colors and price.

- providers  
  Stores supplier information such as name, NIF, phone number and address.

### Relationships

- Each client stores their purchases inside "last_shoppings"
- Each purchase references a product (glasses) using ObjectId
- Each product references a provider using ObjectId

### Data Model Explanation

- Purchase history is embedded inside the client to match the UI and allow fast access
- References are used to connect collections and avoid duplicating core data
- MongoDB ObjectId is used to link documents between collections

---

## Exercise 2 – Optics Management (Product View)

This exercise represents the same system but from the product (glasses) point of view.

### New Approach

- Each pair of glasses stores a list of clients who bought it
- This is implemented using the field "bought_by"

### Relationships

- Glasses reference their provider using ObjectId (same as Exercise 1)
- Glasses include a list of clients using "bought_by"
- Each element in "bought_by" references a client using ObjectId

### Data Model Explanation

- Exercise 1 focuses on:  
  client → purchases → glasses

- Exercise 2 focuses on:  
  glasses → bought_by → clients

- This creates a bidirectional relationship between clients and glasses

- Client data is not duplicated inside glasses, only references are stored

---

## Diagram

The diagram was generated using MongoDB Compass (Data Modeling section).

---
## Exercise 1 – Food Delivery (Level 2)

This exercise represents a database for an online food ordering system.

### Collections

- clients  
  Stores customer information, including personal data, address and contact details.

- products  
  Contains the product catalog (pizzas, burgers and drinks) with name, description, image and price.

- pizzaCategories  
  Stores pizza categories separately to allow changes without affecting products.

- orders  
  Stores customer orders with date, type (delivery or pickup), products, total price and additional notes.

- stores  
  Stores information about each shop that manages orders.

- employees  
  Stores employee data (cook or delivery person) and the store they belong to.

### Relationships

- Each client can make multiple orders  
- Each order references one client using ObjectId

- Each order is managed by one store  
- Each store can manage multiple orders

- Each store has multiple employees  
- Each employee references one store

- Delivery orders include the employee responsible for delivery  
- This is stored inside the order (delivery.employeeId)

- Each pizza references a category  
- Categories can be updated without modifying products

### Data Model Explanation

- Orders store their products embedded (name, price, quantity)

- This allows:
  - keeping the order independent from product changes  
  - preserving the exact state of the order  
  - faster access without extra queries  

- References (ObjectId) are used for:
  - clients  
  - stores  
  - employees  
  - pizza categories  

- The model separates:
  - products → current catalog  
  - orders → historical data  

- Delivery information is only included when the order is for delivery
