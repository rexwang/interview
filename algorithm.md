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
##### Quick Sort
Quick Sork is unstable sorting algorithm. It does not require extra memory space, it's inplace sorting.
```
function qsort(A, lo, hi) {
  if (lo < hi) {
    p = partition(A, lo, hi);
    qsort(A, lo, p - 1);
    qsort(A, p + 1, hi);
  }
}

function partition(A, lo, hi) {
  var pivotIndex = lo,
      pivotValue = A[pivotIndex],
      storeIndex;
      
  // Put the chosen pivot at A[hi]
  swap(A, pivotIndex, hi);
  storeIndex = lo;
  
  for (var i = lo; i < hi; i++) {
    if (A[i] <= pivotValue) {
      swap(A, i, storeIndex);
      storeIndex++;
    }
  }
  
  // move the pivot to its final place
  swap(A, storeIndex, hi);
  
  return storeIndex;
}

function swap(A, a, b) {
  var temp = A[a];
  A[a] = A[b];
  A[b] = temp;
}
```
##### Heapsort
```
funtion heapsort(A, count) {
  var end = count - 1;
  heapify(A, count);
  while (end > 0) {
    swap(A, end, 0);
    // heap size reduced by 1.
    end--;
    // the swap ruined the heap order, restore it.
    shiftDown(A, 0, end);
  }
}

function heapify(A, count) {
  // start is the last parent node.
  // the last element in a 0-base array is at index count-1; find the parent of that element
  var start = Math.floor((count - 2) / 2);
  
  while (start >= 0) {
    shiftDown(A, start, count - 1);
    // go to next parent node.
    start--;
  }
  
  // after shifting down the root all nodes/elements are in heap order
}

function shiftDown(A, start, end) {
  var root = start,
      child,
      swa;
    
  // while the root has at least one child  
  while (root * 2 + 1 <= end) {
    child = root * 2 + 1; // left child
    swa = root; // keep track of child to swap with
    
    if (A[swa] < A[child]) {
      swa = child;
    }
    
    // if there is a right child and that child is greater
    if (child + 1 <= end && A[swa] <= A[child+1]) {
      swa = child + 1;
    }
    
    if (swa == root) {
      // the root holds the largest element.
      return;
    } else {
      swap(A, root, swa);
      // update root index
      root = swa;
    }
  }
}
```
