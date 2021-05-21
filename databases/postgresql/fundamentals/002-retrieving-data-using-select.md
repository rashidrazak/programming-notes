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

## Calculated Column

We can do mathematical calculation in our query as such:

```postgresql
SELECT name, population / area AS population_density
FROM cities;
```