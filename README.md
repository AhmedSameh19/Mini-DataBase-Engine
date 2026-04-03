# Mini DataBase Engine

A small Java-based database engine that stores tables and pages on disk, supports B+ tree indexing, and exposes basic table operations such as create, insert, update, delete, and select.

## Project Layout

- `starter-code/` - Java source files for the engine
- `starter-code/resources/DBApp.config` - page size configuration
- `metadata.csv` - table metadata catalog
- `Tables/` - serialized table objects
- `Pages/` - serialized data pages
- `Index/` - serialized B+ tree indexes

## Main Classes

- `DBApp` - entry point and high-level table/index operations
- `Table` - manages pages, inserts, updates, deletes, and indexes
- `Page` - stores a fixed number of rows
- `Row` - wraps a record and provides clustering-key comparison
- `BPlusTree` - in-memory B+ tree implementation used for indexed columns
- `SQLTerm` - query helper used for select operations

## Supported Operations

The engine currently supports:

- `createTable`
- `createIndex`
- `insertIntoTable`
- `updateTable`
- `deleteFromTable`
- `selectFromTable`

## Requirements

- Java 8 or later
- A terminal with `javac` and `java` available

## Configuration

The page size is controlled by `starter-code/resources/DBApp.config`:

```properties
MaximumRowsCountinPage=4
```

The value must be greater than 3.

## Build and Run

From the repository root:

```bash
cd starter-code
javac *.java
java DBApp
```

## Important Note for Linux

The current `DBApp.init()` implementation loads the config file using a Windows-style path:

```java
starter-code\resources\DBApp.config
```

On Linux, that path will not resolve correctly as-is. If you want to run the starter code on Linux, update that path to use `/` separators or adjust the working directory/path handling in `DBApp.java`.

## Storage Files

At runtime, the engine writes serialized data to:

- `Tables/<table-name>.class`
- `Pages/<table-name><page-number>.class`
- `Index/<index-name>.class`

The metadata catalog is stored in `metadata.csv`.

## Example Usage

A simple flow is:

1. Create a table with a clustering key.
2. Insert rows into the table.
3. Optionally create an index on a column.
4. Query, update, or delete rows through `DBApp`.

## Notes

- The project uses default-package Java classes, so compile from the `starter-code/` directory.
- The `main` method in `DBApp` contains a small manual test sequence.
