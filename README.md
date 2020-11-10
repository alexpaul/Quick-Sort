# Quick-Sort

Quick sort algorithm in Swift. 

Quick sorting algorithm uses a divide and conquer approach a bit similar to merge sort. Given an unsorted array and a partitioning method listed below a pivot is calculated. The array is divided into two sections and the process is continued on each sub array until the array is sorted. 

## Partitioning methods 

* Naive approach
* Hoare's Partitioning
* Lomuto's Partitioning
* Dutch Flag 

## A naive approach 

```swift 
func quickSortNaive(_ arr: [Int]) -> [Int] {
  guard arr.count > 1 else {
    return arr
  }
  let pivot = arr[arr.count / 2] // pick the middle element
  let left = arr.filter { $0 < pivot }
  let equal = arr.filter { $0 == pivot }
  let right = arr.filter { $0 > pivot }
  return quickSortNaive(left) + equal + quickSortNaive(right)
}

let sortedArr = quickSortNaive([-33, 0, -4, -20, 59, 17, 29]) 
print(sortedArr) // [-33, -20, -4, 0, 17, 29, 59]
```

## Quick sort implmentation using Lomuto's Partitioning 

The Lomuto's algorithm chooses the last index when calculating the new pivot point for partitioning the array. 

Runtime: `O(n log n)` uses a divide and conquer approach similar to Merge sort.    
Space: `O(1)` sorts array in-place, no additional arrays are created as opposed to Merge sort or the naive approach above.       

#### Lomuto's Partiioning Algorithm

Steps of the Lomuto's algorithm: 

1. Set the pivot by using the last element of the array. 
2. Iterate through the array. 
3. If the current element is less than or equal to the pivot swap the index with the high element. 
4. If a swap is performed increment the index. 
5. Swap the index and high elements.
6. Return the index. This index will be used as the new pivot for dividing the array into left and right sub arrays. 

![quick sort sketch](https://user-images.githubusercontent.com/1819208/98613985-77dff600-22c5-11eb-80c3-2dd2816e4d26.jpg)


#### Quick sort algorithm using Lomuto

1. If the low index is less than high index we need to perform the following steps recursively. 
2. Find a new pivot using Lomuto's partitioning. 
3. Sort the left array recursively 
4. Sort the right array recursivly. 
5. Since Quick sort is done in place the algorithm is done when low index is no longer less than high. 

```swift 
// Quick Sort

// First part is using Lomuto's Partitioning to find the index of the new pivot
func lomutoPartitioning(_ arr: inout [Int], low: Int, high: Int) -> Int {
  /*
   Steps of Lomuto's Partitioning
   1. Use the last element as the pivot
   2. Iterate the array with i and j variables
   3. If element at j is less than the pivot then swap i and j, increment i
   4. Swap i and the high indices
   5. Return i (new pivot to divide the array using recursion)
  */
  var i = low
  // 1
  let pivot = arr[high] // last element
  
  // 2
  for j in low..<high {
    // 3
    if arr[j] <= pivot {
      // swap
      arr.swapAt(i, j)
      i += 1
    }
  }
  
  // 5
  arr.swapAt(i, high)
  
  // 6
  return i
}


// Second part is using recursion to break up array into subarrays while sorting in place
func quicksort(_ arr: inout [Int], low: Int, high: Int) {
  /*
   Steps for Quick sort using Lomuto's partitioning
   
   1. Calculate the new pivot
   2. left array recursive call will be low, pivot - 1
   3. right array recursive call will be pivot + 1, high
  */
  if low < high { // if there are greater than 1 value keep sorting
    // 1
    let pivot = lomutoPartitioning(&arr, low: low, high: high)
    
    // 2
    quicksort(&arr, low: low, high: pivot - 1)
    
    // 3
    quicksort(&arr, low: pivot + 1, high: high)
  }
}

var inputArr = [3, 0, -5, 1, -10, 3]
quicksort(&inputArr, low: 0, high: inputArr.count - 1)
print(inputArr)
```

## Resources 

1. [Wikipedia - Quicksort](https://en.wikipedia.org/wiki/Quicksort)
1. [RW - Swift Algorithm Club](https://github.com/raywenderlich/swift-algorithm-club/tree/master/Quicksort)
