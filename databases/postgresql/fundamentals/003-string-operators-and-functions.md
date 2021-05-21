# String Operators and Functions

## Operators and Functions

`||` - Concatenate strings

`CONCAT()` - Concatenate string

`LOWER()` - Gives lower case string

`UPPER()` - Gives upper case string

`LENGTH()` - Gives number of characters in a string

## String concatenation example

```postgresql
SELECT name || ', ' || country AS location FROM cities;
```

```postgresql
SELECT CONCAT(name, ', ', country) AS location FROM cities;
```

```postgresql
SELECT 
  CONCAT(UPPER(name), ', ', UPPER(country)) AS location
FROM
  cities;
```

```postgresql
SELECT
  UPPER(CONCAT(name, ', ', country)) AS location
FROM
  cities;
```