# Algorithm Interview Questions

### Array Sorting

##### Selection sort (O^2)
```

function selectionSort(A) {
  var temp,
      i,
      j,
      iMin;

  for (i = 0; i < A.length-1; i++) {
    // assume the min is the first element
    iMin = i;
    for (j = i+1; j < A.length; j++) {
      if (A[j] < A[iMin]) {
        iMin = j;
      }
    }
    
    if (iMin != i) {
      temp = A[i];
      A[i] = A[iMin];
      A[iMin] = temp;
    }
  }
  
  return A;
}
```
##### Insertion Sort
```
function insertionSort(A) {
  var i,
      j,
      temp;
  
  for (i = 0; i < A.length - 1; i++) {
    for (j = i + 1; j < A.length; j++) {
      if (A[i] > A[j]) {
        temp = A[i];
        A[i] = A[j];
        A[j] = temp;
      }
    }
  }
  
  return A;
}
```
##### Merge Sort (Onlogn)
```
function merge_sort(A) {
  // Base case. A list of 0 or 1 element is sorted.
  if (A.length <= 1) {
    return A;
  }
  
  // Recursive case. First divide the list into sublists.
  var left = [],
      right = [],
      middle = Math.floor(A.length / 2);
      
  for (var i = 0; i < middle; i++) {
    left.push(A[i]);
  }
  for (var j = middle; j < A.length; j++) {
    right.push(A[j]);
  }
  
  // Recursively sort both sublists
  left = merge_sort(left);
  right = merge_sort(right);
  
  // Merge the now-sorted lists
  return merge(left, right);
}

function merge(left, right) {
  var result = [];
  
  while (left.length > 0 && right.length > 0) {
    if (left[0] <= right[0]) {
      result.push(left[0]);
      left.shift();
    } else {
      result.push(right[0]);
      right.shift();
    }
  }
  
  // either left or right may have elements left
  while (left.length > 0) {
    result.push(left[0]);
    left.shift();
  }
  while (right.length > 0) {
    result.push(right[0]);
    right.shift();
  }
  
  return result;
}
```
