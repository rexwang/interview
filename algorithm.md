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
