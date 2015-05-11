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
for i <- 1 to length(A) - 1
    j <- i
    while j > 0 and A[j-1] > A[j]
      swap A[j] and A[j-1]
      j <- j - 1
    end while
end for
```
