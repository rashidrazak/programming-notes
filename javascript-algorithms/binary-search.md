# Binary Search

Binary search is a much faster form of search when compared to linear search. Rather than eliminating one element at a time, we can eliminate half of the remaining  elements at a time.

Bad news, it only works on sorted arrays.

The idea is to use `Divide and Conquer`.

Using binary search, in best case scenario, time complexity-wise, we will get O(1). The worst case scenario and average case scenario, we will get O(log n).

## Binary Search Pseudocode

- Write a function that accepts 2 arguments:
  - The array contaning the list
  - What we want to search
- Create a left pointer at the start of the array, and a right pointer at the end of the array
- While the left pointer comes before the right pointer
  - Create a pointer in the middle
  - If we find the value we want, return the index
  - If the value is too small, move the left pointer up
  - If the value is too large, move the right pointer down
- If we never find the value, return -1

## Binary Search Example

This is an example implementation of binary search.

Example 1

```javascript
function binarySearch(array, toFind) {
  let left = 0
  let right = array.length - 1
  let middle = Math.floor(array.length / 2)

  while (left < right) {
    if (array[left] === toFind) return left
    if (array[right] === toFind) return right
    if (array[middle] === toFind) return middle
    if (array[middle] < toFind) left = middle + 1
    if (array[middle] > toFind) right = middle - 1
    middle = Math.floor((right - left) / 2 + left)
  }

  return -1
}

let result = binarySearch([1,2,3,4,5,6,7,8,9], 10)
console.log(result)
```

Example 2

```javascript
function binarySearch(arr, elem) {
  let start = 0
  let end = arr.length - 1
  let middle = Math.floor((start + end) / 2)
  while(arr[middle] !== elem && start <= end) {
    if(elem < arr[middle]) end = middle - 1
    else start = middle + 1
    middle = Math.floor((start + end) / 2)
  }
  return arr[middle] === elem ? middle : -1
}

let result = binarySearch([2,5,6,9,13,15,28,30], 103)
console.log(result)
```