# manufacturing-data-warehouse
Manufacturing Data Warehouse for Inventory, BOM, and Purchasing Management in a CNC Machine Shop

## Overview
This project presents a manufacturing data warehouse designed for a CNC machine shop producing airgun components and aftermarket accessories.

The system addresses operational challenges such as manual inventory tracking, lack of transaction history, and undocumented product structures. By implementing a structured database for BOM, inventory transactions, and purchasing, the system improves inventory visibility, reduces dependency on manual knowledge, and supports scalable shop floor operations.

---

## Business Context
The database is designed for a small manufacturing business where most operational information is managed manually or relies on the owner's experience. 

Inventory data, product structures, and outsourcing processes are not centrally organized and are often scattered across different tools such as Shopify or informal records.

---

## Key Challenges
- No formal inventory transaction history  
- Manual inventory tracking with low visibility  
- BOM knowledge dependent on the owner  
- Difficulty identifying production bottlenecks  
- Fragmented data across systems (e.g., Shopify, spreadsheets)  

---

## Solution
The system introduces a structured manufacturing database that includes:

- **Bill of Materials (BOM)** to define product structures  
- **InventoryTransaction** to track all inventory movements  
- **InventoryOnHand** to maintain current stock levels  
- **Purchase Order system** to manage suppliers and outsourcing  

Forms and reports allow users to:
- Record inventory movements  
- View product structures  
- Manage purchasing operations  

---

## Business Impact
- Reduces reliance on manual knowledge and memory  
- Improves inventory visibility and traceability  
- Enables faster production planning  
- Supports onboarding of new employees  
- Provides foundation for future system integration (e.g., Shopify API)  

---

## Database Design

### Core Entities
- Products  
- Bill of Materials (BOM)  
- InventoryTransaction  
- InventoryOnHand  
- Purchase Orders and PO Details  
- Partners (Suppliers)  
- Employees  
- Categories  

---

## Relational Schema

Customers(cusID PK, CustomerType, CompanyName, CusName, CusTitle, Email, Phone, Address, City, Region, PostalCode, Country, PaymentTerms, Note)

Orders(oID PK, cusID FK, sID FK, eID FK, oDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, ShipCountry)

OD_Details(odID PK, oID FK, pID FK, fgID FK, UnitPrice, Quantity, Discount)

Shippers(sID PK, CompanyName, Phone, City, Email)

Products(pID PK, cID FK, pName, pType, Series, MAP, DealerPrice, StandardCost, Discontinued, MaterialType, MaterialSize, MaterialUnitCost, LastPurchasedPrice, OutsourceCost)

InventoryOnHand(ihID PK, pID FK, Quantity, LastUpdatedDate)

InventoryTransaction(itID PK, pID FK, TransactionDate, TransactionType, QtyChange)

BOM(bomID PK, parentpID FK, childpID FK, Quantity)

Employees(eID PK, eName, Role)

Partners(parID PK, CompanyName, Par_Type, Supplier, Subcontractor, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Email, Website)

PO(poID PK, parID FK, eID FK, OrderDate, ExpectedDate, TotalAmount, Status, PaymentTerms)

PO_Details(podID PK, poID FK, pID FK, UnitPrice, Quantity, ReceivedQuantity, IsClosed)

Categories(cID PK, cName, Description)

---

## Screenshots

### ER Diagram
![ERD](images/erd.png)

### Forms (BOM Main Form & Subform)
![Forms](images/forms.png)

### Reports
![Reports](images/reports.png)

---

## Reflection

### What Went Well
- Designed a practical BOM structure using main form and subform  
- Successfully implemented relationships between inventory and transaction tables  
- Improved debugging and problem-solving skills through Access and VBA issues  

### Challenges
- Difficulty filtering BOM reports due to parent-child relationship structure  
- Balancing conceptual design with Access implementation  
- Limited error visibility in Microsoft Access  

### Improvements
- Define business workflow before database design  
- Automate inventory updates using VBA  
- Expand to SQL-based systems and BI tools such as Power BI  

---

## Future Enhancements
- Integrate with Shopify via API  
- Add order management system (Orders, OrderDetails)  
- Build dashboards using Power BI  
- Automate inventory updates from transaction records  

---

## Tools Used
- Microsoft Access  
- SQL  
- Data Modeling (ERD)  
