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













