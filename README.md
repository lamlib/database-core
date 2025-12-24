# Database Core
The knowledge for working with database

## Data Type for Common RDBMS

### MySQL
### MSSQL
*String Data Type*
| Data type      | Description                                                               | Max char length | Storage                                                   |
| -------------- | ------------------------------------------------------------------------- | --------------- | --------------------------------------------------------- |
| char(n)        | Fixed-length non-Unicode character data(n must be between 1 and 8000)     | 8,000           | n bytes (uses one byte for each character)                |
| varchar(n)     | Variable-length non-Unicode character data (n must be between 1 and 8000) | 8,000           | n bytes + 2 bytes                                         |
| varchar(max)   | Variable-length non-Unicode character data                                |                 | up to 2GB                                                 |
| nchar(n)       | Fixed-length Unicode character data (n must be between 1 and 4000)        | 4,000           | 2 * n bytes (uses two bytes for each character)           |
| nvarchar(n)    | Variable-length Unicode character data(n must be between 1 and 4000)      | 4,000           | 2 * n bytes + 2 bytes (uses two bytes for each character) |
| nvarchar(max)  | Variable-length Unicode character data                                    |                 | up to 2 GB                                                |
| binary(n)      | Fixed-length binary data(n must be between 1 and 8000)                    | 8,000           | n bytes                                                   |
| varbinary(n)   | Variable-length binary data (n must be between 1 and 8000)                | 8,000           | actual length of data entered + 2 bytes                   |
| varbinary(max) | Variable-length binary data                                               | 2GB             |                                                           |


