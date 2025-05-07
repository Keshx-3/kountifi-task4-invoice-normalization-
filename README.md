# kountifi-task4-invoice-normalization

A Python utility to normalize inconsistently formatted invoice data from JSON files into a standardized format suitable for processing by LLMs, analytics systems, or other applications.

## Problem Addressed

Invoice data often comes in various inconsistent formats with:
- Different field names for the same information (e.g., `inv_no`, `invoice_no`, `InvoiceNumber`)
- Diverse date formats (`YYYY-MM-DD`, `MM/DD/YYYY`, `DD-MM-YYYY`, etc.)
- Monetary amounts with or without currency symbols
- Inconsistent currency notations
- Empty fields or misspelled keys

This utility standardizes all these variations into a consistent format.

## Features

- **Key Normalization**: Maps variant field names to standard names
- **Date Parsing**: Converts various date formats to ISO standard (`YYYY-MM-DD`)
- **Amount Cleaning**: Strips currency symbols and converts to float values
- **Currency Standardization**: Normalizes currency codes to standard format
- **Missing Data Handling**: Preserves null values and handles missing fields gracefully

## Installation

No special installation required beyond standard Python 3:

## Input Format 

[
  {
    "invoice_no": "INV-001",
    "date_of_invoice": "01/15/2023",
    "total": "$1,250.00",
    "curr": "$"
  },
  {
    "inv_no": "INV-002",
    "inv_date": "2023-01-20",
    "amount_due": "1500",
    "currency_code": "USD"
  }
]


## Output

[
  {
    "invoice_number": "INV-001",
    "date": "2023-01-15",
    "amount": 1250.0,
    "currency": "USD"
  },
  {
    "invoice_number": "INV-002",
    "date": "2023-01-20",
    "amount": 1500.0,
    "currency": "USD"
  }
]


## Field Mapping

The script normalizes the following key fields:

| Field Type     | Input Variations                         | Normalized To     |
|----------------|-------------------------------------------|-------------------|
| Invoice Number | `invoice_no`, `inv_no`, `invoiceNumber`  | `invoice_number`  |
| Amount         | `amount_due`, `total`, `amt`             | `amount`          |
| Date           | `date_of_invoice`, `inv_date`            | `date`            |
| Currency       | `curr`, `currency_code`                  | `currency`        |



