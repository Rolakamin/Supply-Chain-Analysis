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


### 📊 Dataset Summary

The dataset consists of **five interrelated tables**, covering customer details, product inventory, supplier information, and order transactions. Together, they support end-to-end analysis of the supply chain, with a particular focus on **Port Harcourt** market fulfillment.

| Table Name     | Description                                                   | Rows    | Columns |
|----------------|---------------------------------------------------------------|---------|---------|
| `Customers`    | Customer profiles including registration date, location, and segment     | 15,212  | 12      |
| `Orders`       | All order-level data, including delivery dates, payment info, and shipping location | 75,000  | 19      |
| `OrderItems`   | Line-item details for each order, including product, quantity, and return status   | 163,750 | 7       |
| `Products`     | Product catalog with pricing, inventory level, category, and status      | 200     | 9       |
| `Suppliers`    | Information on 15 suppliers including contact info, rating, and business region     | 15      | 8       |






