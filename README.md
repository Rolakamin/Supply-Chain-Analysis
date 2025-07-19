# Supply Chain Analysis

## Project Overview

This project analyzes supply chain performance and fulfillment issues for an e-commerce company based in Port Harcourt, Nigeria.  
The goal is to uncover operational inefficiencies related to product availability, order delays, and supplier performance that may be negatively impacting customer satisfaction, especially among newly acquired customers in the Port Harcourt market.

### Problem Statement

Rapid sales growth in the Port Harcourt region has exposed critical bottlenecks in **product availability** and **order fulfillment**, resulting in **cancellations, delays, and potential customer churn**, especially among newly acquired customers.

### Business Objectives

This analysis aims to provide actionable insights for the stakeholders, the Country Manager and Head of E-commerce Operations (Nigeria), by addressing the following key questions:

**1. Identify Key Product Availability Gaps**

Which of the 200 products are most frequently out of stock or are major contributors to Cancelled orders, 
especially for shipments to Port Harcourt and surrounding areas, despite the high order volume?

**2. Assess the Impact on Recent Customer Cohorts**

Determine whether fulfillment issues, such as **significant delivery delays** (where **ActualDeliveryDate** far exceeds **ExpectedDeliveryDate**) or **high cancellation rates**, are affecting new customers (those  who registered after **March 1, 2024**) more than existing ones.  
Also, assess whether these fulfillment challenges are correlated with **lower initial repeat purchase rates** among this new customer segment.

 **3. Identify Supplier-Related Fulfillment Constraints**  
 
Among the 15 suppliers, determine which ones are most frequently associated with products that:
 
- Are often **out of stock** or have low inventory (**StockQuantity**)
- Have a high number of **returns**, suggesting potential quality issues (**ReturnStatus**)
- Contribute to **cancellations or failed deliveries**, particularly for shipments to **Port Harcourt**

The goal is to highlight suppliers whose products are consistently involved in fulfillment breakdowns and may require closer management or escalation.


### Dataset Summary

The dataset consists of **five interrelated tables**, covering customer details, product inventory, supplier information, and order transactions. Together, they support end-to-end analysis of the supply chain, with a particular focus on **Port Harcourt** market fulfillment.

| Table Name     | Description                                                   | Rows    | Columns |
|----------------|---------------------------------------------------------------|---------|---------|
| `Customers`    | Customer profiles including registration date, location, and segment     | 15,212  | 12      |
| `Orders`       | All order-level data, including delivery dates, payment info, and shipping location | 75,000  | 19      |
| `OrderItems`   | Line-item details for each order, including product, quantity, and return status   | 163,750 | 7       |
| `Products`     | Product catalog with pricing, inventory level, category, and status      | 200     | 9       |
| `Suppliers`    | Information on 15 suppliers including contact info, rating, and business region     | 15      | 8       |


## Data Dictionary 



### Customers Table

| Column Name       | Description                                                |
|-------------------|------------------------------------------------------------|
| CustomerID        | Unique identifier for each customer                        |
| FirstName         | Customer’s first name                                      |
| LastName          | Customer’s last name                                       |
| Email             | Customer's email address                                   |
| Address           | Full residential/street address                            |
| City              | Customer’s city (e.g., Lagos, Port Harcourt)               |
| PostalCode        | Postal/zip code                                            |
| RegistrationDate  | Date the customer registered on the platform               |
| LastLoginDate     | Timestamp of the most recent login                         |
| CustomerSegment   | Loyalty or marketing segment (e.g., Gold, New, VIP)        |
| DateOfBirth       | Customer’s birth date                                      |
| Phone             | Customer’s phone number                                    |



### Orders Table

| Column Name            | Description                                                              |
|------------------------|--------------------------------------------------------------------------|
| OrderID                | Unique identifier for each order                                        |
| CustomerID             | ID of the customer who placed the order                                 |
| OrderDate              | Date the order was placed                                               |
| ShipDate               | Date the order was shipped (if applicable)                              |
| ExpectedDeliveryDate   | Date the order was expected to be delivered                             |
| ActualDeliveryDate     | Date the order was actually delivered (if delivered)                    |
| OrderStatus            | Current status of the order (e.g., Delivered, Canceled, Returned)       |
| ShippingMethod         | Delivery method used (e.g., Standard, Express, Local Pickup)            |
| ShippingCost           | Cost of shipping (in Nigerian Naira - NGN)                              |
| ShippingAddress        | Full shipping address                                                   |
| ShippingCity           | City where the order was shipped                                        |
| ShippingState          | State where the order was shipped                                       |
| ShippingPostalCode     | Postal code of the delivery address                                     |
| ShippingCountry        | Country of the delivery address (typically Nigeria)                     |
| PaymentMethod          | Payment method used by the customer (e.g., Card, Bank Transfer)         |
| PaymentStatus          | Status of payment (e.g., Paid, Failed, Pending)                         |
| DiscountCode           | Discount or promo code applied to the order (if any)                    |
| DiscountAmount         | Value of the discount applied (in NGN)                                  |
| TotalAmount            | Total amount of the order after discounts (in NGN)                      |



### OrderItems Table

 | Column Name        | Description                                                              |
|--------------------|--------------------------------------------------------------------------|
| OrderItemID        | Unique identifier for each order line item                              |
| OrderID            | ID of the order this item belongs to                                     |
| ProductID          | ID of the product purchased                                              |
| Quantity           | Number of units of the product ordered                                   |
| UnitPrice          | Price of a single unit at the time of purchase (in NGN)                  |
| TotalItemPrice     | Total price for the item (Quantity × UnitPrice)                          |
| ReturnStatus       | Status of the item return (e.g., Returned, Not Returned, Approved)       |



### Products Table

| Column Name      | Description                                                              |
|------------------|--------------------------------------------------------------------------|
| ProductID        | Unique identifier for each product                                       |
| ProductName      | Name or title of the product                                             |
| Category         | Product category (e.g., Health & Beauty, Electronics)                    |
| SupplierID       | ID of the supplier providing the product                                 |
| UnitPrice        | Price per unit of the product (in NGN)                                   |
| StockQuantity    | Current quantity in stock                                                |
| ProductStatus    | Status of the product (e.g., Active, Discontinued, OutOfStock)           |
| LaunchDate       | Date the product was launched or made available                          |
| Weight           | Product weight in kilograms (kg)                                         |



### Suppliers Table

| Column Name       | Description                                                              |
|-------------------|--------------------------------------------------------------------------|
| SupplierID        | Unique identifier for each supplier                                      |
| SupplierName      | Name of the supplier or company                                          |
| Country           | Country where the supplier is located                                    |
| Region            | Global region (e.g., Africa, Europe, North America)                      |
| ContactEmail      | Supplier’s primary email contact                                         |
| Phone             | Supplier’s phone number                                                  |
| YearsInBusiness   | Number of years the supplier has been in operation                       |
| SupplierRating    | Supplier's performance rating or quality tier (e.g., 5-star, Awaiting)   |



## Data Cleaning

The dataset underwent light cleaning and transformation using **Excel Power Query** before being imported into **Microsoft SQL Server**.  
The objective was to address obvious inconsistencies, normalize formats, and prepare the data for SQL-based analysis, while deferring complex validation, such as invalid dates, duplicate records, and outlier detection, as well as business rule–driven filtering, to SQL.

### Customers Table

- Trimmed all text fields to remove leading/trailing spaces (e.g., **CustomerID**, **Email**, **City**).

- Standardized **CustomerSegment** values (e.g., variants like **gold**, **GOLD_v2**, **Gold (old)** were normalized to **Gold)**. A custom column was created to normalize the categories using the following Power Query formula:

 ```
let segment = Text.Lower(Text.Trim([CustomerSegment])) in
    if Text.StartsWith(segment, "bronze") then "Bronze" else
    if Text.StartsWith(segment, "silver") then "Silver" else
    if Text.StartsWith(segment, "gold") then "Gold" else
    if Text.StartsWith(segment, "platinum") then "Platinum" else
    if Text.StartsWith(segment, "standard") or segment = "std." then "Standard" else
    if Text.StartsWith(segment, "vip") then "VIP" else
    if Text.StartsWith(segment, "new") then "New" else
    if segment = "regular" then "Standard" else segment
```

- Replaced placeholder dates **(1/1/1900)** in **DateOfBirth** with **null** using **Replace Value** function.

- Cleaned Phone column, which had mixed formats like **+1-673-409-0301x078**, **(854)220-2272**, **-1643**, **10278**, etc.
A custom formula was used to remove negative and whitespace-only numbers:

```
let phone = Text.Trim([Phone]) in
    if phone = "" or Text.StartsWith(phone, "-") then null else phone
```

- Preserved all null and blank values in fields like Email, PostalCode, LastLoginDate, DateOfBirth, and Phone for downstream handling in SQL.

- Deleted original uncleaned columns and renamed the cleaned versions to their original names for consistency.

### Orders Table

- **Trimmed text columns** such as **OrderID** and **CustomerID** to remove leading and trailing spaces.

#### Date Fields — Parsing Inconsistent Formats

- Many of the date fields were stored as **text** in inconsistent formats (e.g., **03/01/2024**, **2024-03-01 13:59**, **20240301120500**, **Invalid Date String**).  
- To ensure these columns could be queried properly in SQL, they were **parsed and converted to valid **Date types** using Power Query.

---

##### **OrderDate** 
- The `OrderDate` column was duplicated.
- A custom column was created using:

```
try DateTime.FromText([ParsedOrderDate])
```

- The resulting record was expanded to extract the `Value` field.
- Converted to **Date**.
- The original column was removed to retain only the cleaned version.

 **Parsing** means converting from unstructured text into a valid date format.

---

##### ShipDate and ActualDeliveryDate:
- Followed the same process.
- This safely handled invalid formats and left **null** where conversion failed.

---

#### OrderStatus

- **OrderStatus** values had inconsistent casing and naming like **"DELIVERED_v2"**, **"processing"**, **"Canceled (old)"**.
- Cleaned by trimming and converting to lowercase, then normalizing using:

```
let status = Text.Lower(Text.Trim([OrderStatus])) in
    if Text.Contains(status, "cancel") then "Canceled" else
    if Text.Contains(status, "deliver") then "Delivered" else
    if Text.Contains(status, "partially shipped") then "Partially Shipped" else
    if Text.Contains(status, "pending") then "Pending" else
    if Text.Contains(status, "processing") then "Processing" else
    if Text.Contains(status, "returned") then "Returned" else
    if Text.Contains(status, "shipped") then "Shipped" else status
```

---

#### ShippingMethod

- Contained inconsistent formats like **"Express (Lagos/PH/Abuja)_v2"**, **"std."**, **"LOCAL PICKUP (PH ONLY)"**.
- Trimmed and converted to lowercase, then cleaned using:

```
let method = Text.Lower(Text.Trim([ShippingMethod])) in
    if Text.Contains(method, "express") then "Express" else
    if Text.Contains(method, "pickup") then "Local Pickup" else
    if Text.Contains(method, "interstate") then "Interstate Bus" else
    if Text.Contains(method, "standard") or method = "std" or method = "std." then "Standard" else
    if Text.Contains(method, "regular") then "Regular" else method
```

---

#### ShippingCost

- Column was renamed from **ShippingCost_NGN** to **ShippingCost** for SQL compatibility.

---

#### Address Fields

- **ShippingAddress**, **ShippingCity**, **ShippingState**, and **ShippingCountry** were trimmed for whitespace.
- **ShippingPostalCode** was converted from **Whole Number** to **Text** to preserve formatting and prevent loss of leading zeros.

---

#### PaymentMethod

- Trimmed and lowercased.
- Cleaned using a formula to map variants like **"card (paystack/flutterwave)"**, **"ussd_v2"** into standardized values:

```
let method = Text.Lower(Text.Trim([PaymentMethod])) in
    if Text.Contains(method, "bank transfer") then "Bank Transfer" else
    if Text.Contains(method, "card") then "Card" else
    if Text.Contains(method, "cash") then "Cash on Delivery" else
    if Text.Contains(method, "credit card") then "Credit Card" else
    if Text.Contains(method, "paypal") then "PayPal" else
    if Text.Contains(method, "ussd") then "USSD" else method
```

---

#### PaymentStatus

- Cleaned similarly using this formula:

```
let status = Text.Lower(Text.Trim([PaymentStatus])) in
    if Text.Contains(status, "authorized") then "Authorized" else
    if Text.Contains(status, "failed") then "Failed" else
    if Text.Contains(status, "paid") then "Paid" else
    if Text.Contains(status, "pending payment") then "Pending Payment" else
    if Text.Contains(status, "refunded") then "Refunded" else status
```

---

#### DiscountCode

- Over **63,000 rows** were blank or null. These were preserved to support future analysis of discount usage.

---

#### DiscountAmount

- Renamed from **DiscountAmount_NGN** to `DiscountAmount`.
- Null values were retained to preserve accurate discount history.

---

#### TotalAmount

- Renamed from **TotalAmount_NGN** to **TotalAmount**.
- Rows with **null or 0** values in the **TotalAmount** column were retained to allow for future analysis of incomplete purchases, fully discounted orders, or potential internal test transactions that may have been entered during system testing or data setup.

### OrderItems Table 

- Text columns such as **OrderItemID**, **OrderID**, **ProductID**, and **ReturnStatus** were trimmed to remove leading or trailing whitespace. This ensures clean joins, consistent filtering, and accurate matching during analysis.

- The columns **UnitPriceAtPurchase_NGN** and **TotalItemPrice_NGN** were renamed to **UnitPriceAtPurchase** and **TotalItemPrice** respectively for naming consistency and SQL compatibility.

- Null values in the **ReturnStatus** column were retained to allow analysis of return behavior later in SQL (e.g., to distinguish between returned, approved, or unprocessed items).

- **Negative** or **zero** values in the **Quantity** column were not flagged or filtered in Power Query. These edge cases were left intact for downstream validation in SQL,possibly indicating errors, cancellations, or system test records.

### Products Table

- Trimmed text columns such as `ProductID`, `ProductName`, and `Category` to remove leading and trailing spaces.
  
- Standardized category names using the transformation:
  ```
  Text.Proper(Text.Trim([Category]))
  to fix inconsistent casing (e.g., local crafts, Local Crafts) and remove duplicates caused by trailing spaces.

- Replaced versioned entries using Replace Values, such as:

"Automotive Parts (Old)" → "Automotive Parts"

- Standardized values in ProductStatus using Replace Values, e.g.:

"active" → "Active"

"Active_v2" → "Active"

- Converted LaunchDate column from text to date following the steps below:
  
1. Duplicated the column as ParsedLaunchDate
2. Applied:
 ```  
    try Date.FromText([ParsedLaunchDate])
```
3. Extracted Value from the result
4. Changed data type to Date
5. Replaced the original LaunchDate column

- Renamed **UnitPrice_NGN** column to **UnitPrice**.

- **Null and negative values** in **UnitPrice**, **StockQuantity**, and **Weight** were retained for further analysis in SQL.

### Suppliers Table

- Trimmed text columns: SupplierID, SupplierName, Country, Region, ContactEmail, and Phone.

- Normalized inconsistent values in the SupplierRating column by creating a new column **NormalizedRating** with the following formula:

```
let rating = Text.Lower(Text.Trim([SupplierRating])) in
    if rating = "" then "" else
    if Text.Contains(rating, "1") then "1" else
    if Text.Contains(rating, "2") then "2" else
    if Text.Contains(rating, "3") then "3" else
    if Text.Contains(rating, "4") then "4" else
    if Text.Contains(rating, "5") then "5" else
    if Text.Contains(rating, "awaiting") then "Awaiting Rating" else rating
```
- Deleted the original SupplierRating column

- Renamed **NormalizedRating** to **SupplierRating**

- Removed negative or invalid phone numbers; retained entries with mixed valid formats.

- Null values in **Region**, **Phone**, and **YearsInBusiness** were left for downstream handling in SQL.

## Data Import to Microsoft SQL Server

After light cleaning in Excel Power Query, each table was exported as a **.csv** file and imported into **Microsoft SQL Server** using the **Import Flat File Wizard**.

During the import process:

- Column data types were reviewed and adjusted (e.g., **Date**, **Decimal(18,2)**, **VARCHAR**, **INT**).

- Fields with missing values (e.g., **Phone**, **LastLoginDate**, **TotalAmount**) were set to Allow **Nulls**.

- **Primary key columns** such as **CustomerID**, **OrderID**, **OrderItemID**, and **ProductID** were not allowed to contain nulls, ensuring data integrity.

- After loading, row counts were validated to confirm successful import.

This process ensured the dataset was structurally sound and ready for querying.

## Data Exploration & Validation

After importing the lightly cleaned data into Microsoft SQL Server, an initial exploration was conducted to validate the integrity and quality of the dataset before performing analysis.

### Row Count Verification

Checked the number of rows in each table to confirm they match expected values from the original data (as cleaned in Power Query):

```
SELECT COUNT(*) AS TotalCustomers FROM Customers;
SELECT COUNT(*) AS TotalOrders FROM Orders;
SELECT COUNT(*) AS TotalOrderItems FROM OrderItems;
SELECT COUNT(*) AS TotalProducts FROM Products;
SELECT COUNT(*) AS TotalSuppliers FROM Suppliers;
```

- **The number of rows in each table matched expected values from the original data, confirming complete importation. Results:  Totalcustomers (15212), TotalOrders(75000), TotalOrderItems(163750), TotalProducts(200), TotalSuppliers(15)**

###  Primary Key Integrity Checks

Verified the primary key columns for nulls

```
SELECT COUNT(*) FROM Customers WHERE CustomerID IS NULL;
SELECT COUNT(*) FROM Orders WHERE OrderID IS NULL;
SELECT COUNT(*) FROM OrderItems WHERE OrderItemID IS NULL;
```

- **All primary key fields returned 0 NULLs, confirming primary key integrity**

### Foreign Key Sanity Checks 

Checked whether any foreign keys were missing (e.g., Orders without CustomerID, or OrderItems without ProductID)

```
SELECT COUNT(*) AS NullCustomerID FROM Orders WHERE CustomerID IS NULL;
SELECT COUNT(*) AS NullProductID FROM OrderItems WHERE ProductID IS NULL;
```
- **Both checks returned 0, confirming valid relational structure**

###  Null Value Detection in Key Business Fields

Examined key business-critical fields that should not be null under normal operations.

```
-- Orders
SELECT COUNT(*) AS NullOrderDate FROM Orders WHERE OrderDate IS NULL;
SELECT COUNT(*) AS NullTotalAmount FROM Orders WHERE TotalAmount IS NULL;

-- OrderItems
SELECT COUNT(*) AS NullQuantity FROM OrderItems WHERE Quantity IS NULL;
```
- **Output: OrderDate(3,659 nulls), TotalAmount(679 nulls), Quantity (0 nulls).These rows were retained for further analysis. Null OrderDate or TotalAmount may represent incomplete, test, or cancelled orders**

###  Delivery & Return Gaps

```
-- Orders missing delivery completion
SELECT COUNT(*) AS NullActualDeliveryDate FROM Orders WHERE ActualDeliveryDate IS NULL;

-- Order items with blank return status
SELECT COUNT(*) AS NullOrBlankReturnStatus
FROM OrderItems
WHERE ReturnStatus IS NULL OR RTRIM(LTRIM(ReturnStatus)) = '';
```
- **Output: ActualDeliveryDate(57,084 nulls), ReturnStatus(139,105 blanks or nulls). These values suggest many pending deliveries and unprocessed or irrelevant return statuses**

### Duplicate Checks


```
-- Check for duplicate OrderIDs
SELECT OrderID, COUNT(*) AS DuplicateCount
FROM Orders
GROUP BY OrderID
HAVING COUNT(*) > 1;
```
- **No duplicates were found. This confirms unique OrderID values**

## Data Analysis

**Objective 1:** Identify Key Product Availability Gaps

The goal was to identify which products were frequently unavailable, either because they had no stock or were driving a large number of cancellations, particularly affecting Port Harcourt and surrounding areas.
















