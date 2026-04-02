
# MongoDB Data Modeling – Sprint 2.3

This project contains exercises focused on designing and modeling NoSQL databases using MongoDB.

## Project Structure

nivel1/
  exercici1/
    clientes.json
    glasses.json
    providers.json
    optica_diagrama_mongo.png

## Exercise 1 – Optics Management

This exercise represents a database for an optical store.

### Collections

- clients  
  Stores customer information, including personal data, address and purchase history.

- glasses  
  Contains the product catalog with details such as brand, graduation, colors and price.

- providers  
  Stores supplier information such as name, NIF, phone number and address.

### Relationships

The database uses a hybrid approach:

- Each client stores their purchases inside "last_shoppings"
- Each purchase references a product (glasses) using ObjectId
- Each product references a provider using ObjectId

### Data Model Explanation

- Purchase history is embedded inside the client to match the UI and allow fast access
- References are used to connect collections and avoid duplicating core data
- MongoDB ObjectId is used to link documents between collections

### Diagram

The diagram was generated using MongoDB Compass (Data Modeling section).
