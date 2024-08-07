# Bookstore ER Diagram

This repository contains a Mermaid diagram illustrating the entity-relationship (ER) model for a bookstore system. This README provides an explanation of the relationships and the entities involved in the diagram.

## ER Diagram Overview

The ER diagram captures the relationships between various entities in the bookstore system, such as `Customer`, `Order`, `Book`, `Author`, `Supplier`, and `Inventory`. Each entity has attributes with designated primary keys (PK) and foreign keys (FK).

## Entities and Relationships

### Address
- **Attributes**:
  - `AddressID` (PK)
  - `Street`
  - `City`
  - `PostalCode`
  - `Country`
- **Relationships**:
  - One `Address` is associated with zero or more `Customers`.
  - One `Address` is associated with only one `Supplier`.

### Customer
- **Attributes**:
  - `CustomerID` (PK)
  - `FirstName`
  - `LastName`
  - `Email`
  - `Phone`
  - `AddressID` (FK)
- **Relationships**:
  - One `Customer` places zero or more `Orders`.
  - One `Customer` writes zero or more `BookReviews`.

### Author
- **Attributes**:
  - `AuthorID` (PK)
  - `FirstName`
  - `LastName`
  - `Bio`
- **Relationships**:
  - One `Author` writes zero or more `Books`.

### Book
- **Attributes**:
  - `BookID` (PK)
  - `Title`
  - `Genre`
  - `Price`
  - `AuthorID` (FK)
- **Relationships**:
  - One `Book` receives zero or more `BookReviews`.
  - One `Book` is stocked in one or more `Inventories`.
  - One or more `OrderDetails` are for only one `Book`.

### Order
- **Attributes**:
  - `OrderID` (PK)
  - `OrderDate`
  - `CustomerID` (FK)
- **Relationships**:
  - One `Order` contains one or more `OrderDetails`.

### OrderDetail
- **Attributes**:
  - `OrderDetailID` (PK)
  - `OrderID` (FK)
  - `BookID` (FK)
  - `Quantity`
- **Relationships**:
  - One or more `OrderDetails` are for only one `Book`.

### BookReview
- **Attributes**:
  - `ReviewID` (PK)
  - `BookID` (FK)
  - `CustomerID` (FK)
  - `Rating`
  - `ReviewText`
  - `ReviewDate`
- **Relationships**:
  - One `BookReview` is written by one `Customer`.
  - One `BookReview` is for one `Book`.

### Employee
- **Attributes**:
  - `EmployeeID` (PK)
  - `FirstName`
  - `LastName`
  - `Email`
  - `Phone`
  - `Position`
  - `ManagerID` (FK)
- **Relationships**:
  - One `Manager` manages one or more `Employees`.

### Manager
- **Attributes**:
  - `ManagerID` (PK)
  - `FirstName`
  - `LastName`
- **Relationships**:
  - One `Manager` manages one or more `Employees`.

### Supplier
- **Attributes**:
  - `SupplierID` (PK)
  - `SupplierName`
  - `ContactName`
  - `Phone`
  - `AddressID` (FK)
- **Relationships**:
  - One `Supplier` supplies only one `Inventory`.
  - One `Supplier` is located at only one `Address`.

### Inventory
- **Attributes**:
  - `InventoryID` (PK)
  - `BookID` (FK)
  - `QuantityInStock`
  - `LastRestockDate`
  - `SupplierID` (FK)
- **Relationships**:
  - One `Inventory` is stocked with one or more `Books`.

## How to Read the Diagram

- **Relationships**:
  - `"is located at"`: Indicates where the entity is located.
  - `"places"`: Indicates the customer placing an order.
  - `"contains"`: Indicates the order contains order details.
  - `"for"`: Indicates the order detail is for a book.
  - `"receives"`: Indicates the book receives reviews.
  - `"writes"`: Indicates who writes the reviews or books.
  - `"supplies"`: Indicates the supplier supplies the inventory.
  - `"manages"`: Indicates the management relationship between employees and managers.

Each entity and relationship is described with cardinality notation (`only one`, `one or more`, `zero or more`) to specify the number of instances involved in each relationship. 

```mermaid
  erDiagram
    
    Address only one--zero or more Customer: "is located at"
    
    Customer only one--zero or more Order: "places"
    
    Order only one--one or more OrderDetail: "contains"
    
    OrderDetail one or more--only one Book: "for"

    Book only one--zero or more BookReview: "receives"

    Customer only one--zero or more BookReview: "writes"

    Author only one--zero or more Book: "writes"
    
    Supplier only one--only one Inventory: "supplies"

    Address only one--only one Supplier: "is located at"
    
    Book only one--one or more Inventory: "is stocked in"
    
    Employee one or more--only one Manager: "manages"

    Address {
        int AddressID PK
        string Street
        string City
        string PostalCode
        string Country
    }

    Customer {
        int CustomerID PK
        string FirstName
        string LastName
        string Email
        string Phone
        int AddressID FK
    }
    
    Author {
        int AuthorID PK
        string FirstName
        string LastName
        string Bio
    }
    
    Book {
        int BookID PK
        string Title
        string Genre
        decimal Price
        int AuthorID FK
    }
    
    Order {
        int OrderID PK
        date OrderDate
        int CustomerID FK
    }
    
    OrderDetail {
        int OrderDetailID PK
        int OrderID FK
        int BookID FK
        int Quantity
    }

    BookReview {
        int ReviewID PK
        int BookID FK
        int CustomerID FK
        int Rating
        text ReviewText
        date ReviewDate
    }
    
    Employee {
        int EmployeeID PK
        string FirstName
        string LastName
        string Email
        string Phone
        string Position
        int ManagerID FK
    }

    Manager {
        int ManagerID
        string FirstName
        string LastName
    }
    
    Supplier {
        int SupplierID PK
        string SupplierName
        string ContactName
        string Phone
        int AddressID FK
    }
    
    Inventory {
        int InventoryID PK
        int BookID FK
        int QuantityInStock
        date LastRestockDate
        int SupplierID FK
    }
  ```


## Usage

To visualize the ER diagram using Mermaid, ensure you have a compatible Markdown viewer or editor that supports Mermaid syntax.

```mermaid
erDiagram
    ...
```

Replace the `...` with the provided Mermaid diagram code to see the visual representation.
