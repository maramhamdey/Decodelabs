# Decodelabs

## Project Overview

This document describes the changes made to the original dataset to produce the cleaned version attached. The dataset contains 1,200 orders with information about products, customers, payments, and shipping.

---

## Changes Made

### 1. Added New Columns & Changed 'Date' Column Format:

Two new columns were extracted from the existing `Date` column to make time-based analysis easier:

- **Month** & **year** — extracted from the Date field (e.g., January → 1), (e.g., 2023)

This allows for easier grouping and filtering by time period without parsing dates manually.

---

### 2. Added 'Discount' Column

A new 'Discount' column was created based on the existing 'CouponCode' column to represent the actual discount value applied to each order:

| CouponCode | Discount Value |
|------------|--------------- |
| WINTER15   | 0.15 (15%)     |
| SAVE10     | 0.10 (10%)     |
| FREESHIP   | FREESHIP       |
| *(null)*   | No Discount    |

This makes it easier to calculate the actual discount applied per order without needing to look up coupon values separately.

---

### 3. Added Calculation & Reformatted 'TotalPrice' Column

Using the formula : **=IF(OR(O2="No Discount",O2="FREESHIP"),G2*H2,G2*H2*(1-O2))**

O2--Discount
G2--Quantity
H2--UnitPrice

TO calculate the total price more effeciently having in consideration the discount applied.

The 'TotalPrice' column was also reformatted from a plain numeric value to a currency string format:

- **Before:** `2853.1`
- **After:** `$2,853.10`

This improves readability when presenting or displaying the data.

---

### 4. Handled Missing Values in 'CouponCode'

The original dataset had **309 rows** with no coupon code. These were left as null/empty in `CouponCode` (unchanged), but were handled in the new `Discount` column by filling them with the label 'No Discount' for clarity.

---

## Column Reference (Cleaned File)

| Column           | Description                                             |
|------------------|---------------------------------------------------------|
| OrderID          | Unique identifier for each order                        |
| Date             | Date the order was placed **(reformatted)**             |
| Month            | *(New)* Numeric month extracted from Date               |
| year             | *(New)* Year extracted from Date                        |
| CustomerID       | Unique identifier for the customer                      |
| Product          | Name of the purchased product                           |
| Quantity         | Number of units ordered                                 |
| UnitPrice        | Price per unit                                          |
| ShippingAddress  | Delivery address                                        |
| PaymentMethod    | Payment method used                                     |
| OrderStatus      | Current status of the order                             |
| TrackingNumber   | Shipment tracking number                                |
| ItemsInCart      | Number of items in cart at time of order                |
| CouponCode       | Coupon code applied (if any)                            |
| Discount         | *(New)* Discount value derived from CouponCode          |
| ReferralSource   | How the customer found the store                        |
| TotalPrice       | *(New Calc.)*Total order value (formatted as currency)  |

---

## Tools Used

- Microsoft Excel — data exploration and column additions and calculated columns
- Manual cleaning and formatting

---

*Prepared as part of DecodeLab Data Analytics Training*
