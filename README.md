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

## How to chose the right data type
*String Data Type* 
When have THREE strategies: *Fixed-length or Variable-length*, *Unicode or not*, and *The Size*
1. The choise when using Fixed-length (char, nchar) and Variable-length (varchar, nvarchar)
Rule of Thumb: **The stable of Data Length**.
- Using char/nchart (fixed): When you know that data is allways have them same length or have a small differrent.
  + Eg: National Code (VN, US), Gender (M, F), Status Code (Y, N), Social Identifiation Number.
  + Advantage: Query a litte faster cause by SQL know exactly start position and end position of each line.
- Using varchar/nvarchar (Dynamic): When data length have big different between each record.
  + Eg: Human name, Email Adress, Article content.
  + Advantage: Save the storage space because it using enought byte (bonus 2 byte for management stuff)
2. The choise when using Non-Unicode(char, varchar) and Unicode (nchar, nvarchar)
Rule of Thumb: **Language and Symbol**
- Using group start by "n" (National): When you wanna save Vietnamese, Chinese, Japanish, ..etc  and emoji. (1 unicode character need 2 bytes)
- Using group don't have "n": When you wanna save English, Code Number, or ASCII basic. (Save 50% storage)
3. What the time using `max`?
- Using `(n)number`: When you have a bility to limit the length, eg: Human name is not over 255 character. This, will help SQL optimize sorting and indexing.
- Using `max`: Only using when data reach over 8,000 bytes (about 4,000 Unicode characters). Often using for description detail, article content, or system log. (You can not indexing on `max` in the normal way)
4. Binary and Varbinary
  This don't for text data, this for raw data.
- `binary(n)`: Using for binary string have fixed length (rarely)
- `varbinary(n)`: Using to save hash code, .v.v.
- `varbinary(max)`: Using to save File, Picture, or PDF into database (but modern way is to save file external and only save path file)


