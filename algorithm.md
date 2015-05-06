# Algorithm Interview Questions

### Array Sorting

##### Selection sort (O^2)
```
/* a[0] to a[n-1] is the array to sort */
int i,j;
int iMin;
 
/* advance the position through the entire array */
/*   (could do j < n-1 because single element is also min element) */
for (j = 0; j < n-1; j++) {
    /* find the min element in the unsorted a[j .. n-1] */
 
    /* assume the min is the first element */
    iMin = j;
    /* test against elements after j to find the smallest */
    for ( i = j+1; i < n; i++) {
        /* if this element is less, then it is the new minimum */  
        if (a[i] < a[iMin]) {
            /* found new minimum; remember its index */
            iMin = i;
        }
    }
 
    if(iMin != j) {
        swap(a[j], a[iMin]);
    }
 
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
