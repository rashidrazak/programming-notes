# Linear Search

Simplest way to search for a value in an array by looking at every elements in the array by checking if it is the value that we're looking for.

The time complexity is O(n)

Not the best way to find through a sorted data

Examples of Array prototype methods that are using linear search:
- indexOf
- includes
- find
- findIndex

## Example

This is an example of linear search immitating `indexOf` behaviour:

```javascript
function linearSearch(array, toFind) {
  for (const [index, element] of array.entries()) {
    if (element === toFind) return index
  }

  return -1
}
```