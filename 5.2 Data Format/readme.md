# Data Formatting

## Data Validation
- use drop down list to limit predetermined values

## Merging Multiple Sources
`CONCAT()` function can't process empty spaces. `CONCAT(A1, " ", B2)` will not work 
Instead use `CONCATENATE(A1, " ", B2)`

### SQL Concats
| Function | Usage | Example |
| --- | --- | --- | 
| CONCAT | A function that adds strings together to create new text strings that can be used as unique keys | CONCAT (‘Google’, ‘.com’); |
| CONCAT_WS | A function that adds two or more strings together with a separator | CONCAT_WS (‘ . ’, ‘www’, ‘google’, ‘com’) |
| CONCAT with + |	Adds two or more strings together using the + operator | ‘Google’ + ‘.com’ | 

