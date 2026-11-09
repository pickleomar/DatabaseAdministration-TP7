# TP7 - Data Integration with SSIS

Two working SSIS packages for exporting and consolidating sales across SQL Server, Oracle, PostgreSQL and file formats.

## Exercise 1 - Export to five destinations

`Sales_Export.dtsx` reads SQL Server’s `dbo.Ventes2024` once and uses **Multicast** to distribute its rows to:

- CSV with semicolon separators and a header
- Excel workbook
- Access database
- Oracle XE
- PostgreSQL

**Result:** all five destinations received the same 3 source rows.

## Exercise 2 - Import through FTP

`Import_FTP.dtsx` retrieves a PostgreSQL CSV from an Ubuntu VM and consolidates its contents with local SQL Server sales.

**Control Flow:** FTP Task → Data Flow Task → Execute SQL Task

**Data Flow:** Flat File Source → Derived Column → OLE DB Destination

The transformation converts text to Unicode and adds a `Source` column to identify imported rows.

**Result:** 5 consolidated sales, verified with `GROUP BY Source`:

| Source | Rows |
| --- | ---: |
| PostgreSQL | 3 |
| SQLServer | 2 |

## Environment

- Windows 11: SQL Server, Visual Studio and SSIS
- Ubuntu 24.04: PostgreSQL 16 and vsftpd
- Providers: Microsoft OLE DB Driver, ACE, OraOLEDB and PostgreSQL ODBC

Configuration, screenshots and verification queries are documented in the report.

Running the import package again appends rows. Clear the test destination before repeating the demonstration.
