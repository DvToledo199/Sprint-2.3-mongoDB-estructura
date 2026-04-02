# MongoDB Data Modeling – Sprint 2.3

This project contains exercises focused on designing and modeling NoSQL databases using MongoDB.

## Project Structure

nivel1/
  exercici1/
    clientes.json
    glasses.json
    providers.json
    optica_diagrama_mongo.png

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
