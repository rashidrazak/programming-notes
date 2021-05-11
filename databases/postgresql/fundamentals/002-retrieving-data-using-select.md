# Retrieving Data Using Select

## Retrieve all data from table

```postgresql
SELECT * FROM cities;
```

## Retrieve specific columns only

```postgresql
SELECT name, country, population FROM cities;
```

Note: column name can be repeated multiple times. Example:

```postgresql
SELECT name, name, name FROM cities;
```

