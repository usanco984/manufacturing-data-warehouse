# manufacturing-data-warehouse
Manufacturing Data Warehouse for Inventory, BOM, and Purchasing Management in a CNC Machine Shop

# Manufacturing Data Warehouse for CNC Operations

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

## BOM Structure (Self-Referencing Relationship)
The Bill of Materials (BOM) table is designed using a self-referencing relationship on the Products table.

- `parentpID` represents the finished or parent product  
- `childpID` represents the component or material  

This structure allows the system to represent how products are built from multiple parts, including multi-level assemblies.

Note: In the ER diagram, a duplicated Products table (Products_1) is used as a visual alias to represent this self-join relationship. In the actual implementation, both keys reference the same Products table.

---

## Inventory Design Logic
The system separates inventory into two related entities:

- **InventoryTransaction**: records all inventory movements such as purchasing, production, and adjustments  
- **InventoryOnHand**: maintains the current inventory balance for each product  

This design reflects real-world manufacturing systems, where transaction history is preserved while current stock levels are updated separately.

This approach improves traceability, supports auditing of inventory changes, and allows analysis of inventory flow over time.

---

## Design Considerations
For this project, the database design prioritizes practicality and usability for a small manufacturing environment.

Some attributes related to materials, costs, and outsourcing are stored within the Products table rather than being fully normalized into separate entities. This decision was made to simplify data entry and reduce system complexity for end users.

While further normalization could improve scalability, this structure provides a balanced solution for a small business with limited resources.

---

## Data Flow Overview
The system follows a simple operational flow:

1. Products and BOM define how items are structured  
2. Purchase Orders record procurement from suppliers or partners  
3. InventoryTransaction captures all stock movements  
4. InventoryOnHand reflects the current stock levels  

This flow supports key manufacturing operations such as purchasing, production tracking, and inventory management.

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
![ERD](images/erd.jpg)

---

### BOM Form (Parent–Child Structure)
This form displays the relationship between finished products and their components using a main form and subform structure.

![BOM Form](images/form-bom.png)

---

### Inventory Transaction Form
This form records all inventory movements, including purchases, production, and adjustments.

![Inventory Form](images/form-inventory.png)

---

### Purchase Order Form
This form is used to manage supplier transactions and outsourcing processes.

![PO Form](images/form-po.png)

---

### Sample Report
This report provides a structured view of operational data for analysis and tracking.

![Report](images/report-inventory.png)

---

## Reflection

### Project Strengths
- Designed a practical BOM structure using main form and subform  
- Successfully implemented relationships between inventory and transaction tables  
- Improved debugging and problem-solving skills through Access and VBA issues  

### Limitations
- Difficulty filtering BOM reports due to parent-child relationship structure  
- Balancing conceptual design with Access implementation  
- Limited error visibility in Microsoft Access  

### Improvements
- Define business workflow before database design  
- Automate inventory updates using VBA  
- Expand to SQL-based systems and BI tools such as Power BI  

---

## Next Steps
- Integrate with Shopify via API  
- Add order management system (Orders, OrderDetails)  
- Build dashboards using Power BI  
- Automate inventory updates from transaction records  

---

## Tools Used
- Microsoft Access  
- SQL  
- Data Modeling (ERD)

---

Author
Yumi Kuwana
M.S. in Data Analytics in Business
Seattle Pacific University
