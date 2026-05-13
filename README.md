# Document Automation Demo: SQL Server + Word Mail Merge

## Project Overview
This project demonstrates exactly how to translate SQL data into automated documents — pulling live data from SQL Server and merging it into Word templates.

## Skills Demonstrated
- **SQL Server (SSMS):** Wrote queries with JOINs, WHERE filters, and ORDER BY
- **Database Design:** Created Customers and Invoices tables with relationships
- **Word Mail Merge:** Built templates with merge fields («FirstName», «AmountDue», etc.)
- **Live Connection:** Connected Word directly to SQL Server using .odc file

## The Workflow
1. SQL query pulls unpaid customers and their invoices
2. Word template has merge fields mapped to database columns
3. Mail merge generates one letter per customer automatically

## Files in This Repo
| File | Description |
|------|-------------|
| `SQL_Scripts/` | SQL queries to create tables and extract data |
| `Word_Templates/` | LatePaymentLetter.docx, Invoice.docx, Reminder.docx |
| `Sample_Output/` | Generated documents from mail merge |
| `Screenshots/` | Proof of working process |

## Sample SQL Query
```sql
USE DocumentAutomationDemo
GO
SELECT * FROM Customers; --to check the data--

SELECT * FROM Invoices; --to check the data--

SELECT
	c.FirstName,
	c.LastName,
	c.Email,
	c.Address,
	c.City,
	c.PostalCode,
	i.InvoiceNumber,
	i.AmountDue,
	i.DueDate
FROM Customers C
INNER JOIN
	Invoices i ON C.CustomerID = i.CustomerID
WHERE i.isPaid = 0
ORDER BY DueDate ASC;
			
