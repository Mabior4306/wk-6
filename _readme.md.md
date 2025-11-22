# Joins and Relationships Assignment

## Overview
This assignment focuses on using SQL JOINs to retrieve data from multiple related tables, including INNER JOIN, LEFT JOIN, and RIGHT JOIN.

## Assignment Questions and Solutions

### Question 1 🧑‍💼
**Task:** Get the firstName, lastName, email, and officeCode of all employees using an INNER JOIN with the offices table.

**SQL Query:**
```sql
SELECT e.firstName, e.lastName, e.email, e.officeCode
FROM employees e
INNER JOIN offices o ON e.officeCode = o.officeCode;
```

### Question 2 🛍️
**Task:** Get the productName, productVendor, and productLine from the products table using a LEFT JOIN with the productlines table.

**SQL Query:**
```sql
SELECT p.productName, p.productVendor, p.productLine
FROM products p
LEFT JOIN productlines pl ON p.productLine = pl.productLine;
```

### Question 3 📦
**Task:** Retrieve the orderDate, shippedDate, status, and customerNumber for the first 10 orders using a RIGHT JOIN with the customers table.

**SQL Query:**
```sql
SELECT o.orderDate, o.shippedDate, o.status, o.customerNumber
FROM customers c
RIGHT JOIN orders o ON c.customerNumber = o.customerNumber
LIMIT 10;
```

## Submission Instructions
- Save all queries in `answers.sql`.
- Test your queries in MySQL Workbench or another SQL environment.
- Submit both `answers.sql` and this `README.md`.

## Notes
- Use aliases for readability where appropriate.
- Ensure correct use of JOIN types to retrieve the expected results.

---

## GitHub Actions CI/CD Workflow
To automate query validation (example using a basic SQL linter), create the following workflow file at `.github/workflows/sql-validation.yml`:

```yaml
name: SQL Validation

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  sql-lint:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install sqlfluff
        run: |
          python -m pip install --upgrade pip
          pip install sqlfluff

      - name: Lint SQL files
        run: |
          sqlfluff lint answers.sql
```
This workflow lints the `answers.sql` file whenever changes are pushed or a pull request is made to the `main` branch.