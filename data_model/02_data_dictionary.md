**# Data Dictionary – Billing to Cash**



**This document describes the structure and business purpose of each table used in the Billing-to-Cash data model.**



**---**



**## DimCustomer**



**\*\*Grain\*\***  

**One row per customer.**



**\*\*Purpose\*\***  

**Provides customer attributes used for segmentation and exposure analysis.**



**\*\*Key Fields\*\***

**- CustomerID (Primary Key)**

**- CustomerName**

**- CustomerSize**

**- Industry**

**- Country**



**---**



**## DimDate**



**\*\*Grain\*\***  

**One row per calendar date.**



**\*\*Purpose\*\***  

**Supports consistent time-based analysis across all facts.**



**\*\*Key Fields\*\***

**- Date (Primary Key)**

**- Year, Quarter, MonthNumber, MonthName, YearMonth**

**- Day, Weekday, WeekdayNumber, IsWeekend**



**---**



**## FactInvoices**



**\*\*Grain\*\***  

**One row per invoice.**



**\*\*Purpose\*\***  

**Primary source for billed revenue, AR balances, aging, and dispute linkage.**



**\*\*Key Fields\*\***

**- InvoiceID (Primary Key)**

**- CustomerID (Foreign Key)**

**- InvoiceDate**

**- DueDate**

**- InvoiceAmount**

**- InvoiceStatus**



**\*\*Notes\*\***

**- Invoices may have multiple payments.**

**- Invoices may be associated with disputes.**



**---**



**## FactPayments**



**\*\*Grain\*\***  

**One row per payment transaction.**



**\*\*Purpose\*\***  

**Captures cash receipts applied to invoices.**



**\*\*Key Fields\*\***

**- PaymentID (Primary Key)**

**- InvoiceID (Foreign Key)**

**- PaymentDate**

**- PaymentAmount**



**\*\*Notes\*\***

**- Partial payments are supported.**

**- Multiple payments may exist per invoice.**



**---**



**## FactDisputes**



**\*\*Grain\*\***  

**One row per dispute.**



**\*\*Purpose\*\***  

**Tracks disputed invoices and root cause attributes.**



**\*\*Key Fields\*\***

**- DisputeID (Primary Key)**

**- InvoiceID (Foreign Key)**

**- DisputeDate**

**- DisputeReason**

**- DisputeStatus**



**\*\*Notes\*\***

**- Dispute resolution date is not available.**

**- Dispute analysis relies on status rather than duration.**



**---**



**## Modeling Assumptions**



**- One invoice may have multiple payments.**

**- One invoice may be associated with a single active dispute.**

**- Aging is calculated based on invoice due date.**

**- All monetary values are expressed in USD.**



