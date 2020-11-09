# Quick-Sort

Quick sort algorithm in Swift. 

Quick sorting algorithm uses a divide and conquer approach a bit similar to merge sort. Given an unsorted array and a partitioning mehtod listed below a pivot is calculated. The array is divided.....

## Partitioning methods 

* Naive approach
* Lumoto's Partitioning
* Dutch Flag 

## Quick sort implmentation using Lomuto's Partitioning 

The Lomuto's algorithm is used to find a new index to use a the pivot when dividing the array in left and right sides. 

#### Lomuto's Partiioning Algorithm

Steps of the Lomuto's algorithm: 

1. Set the pivot by using the last element of the array. 
2. Iterate through the array. 
3. If the current element is less than or equal to the pivot swap the index with the high element. 
4. If a swap is performed increment the index. 
5. Swap the index and high. 
6. Return the index. This index will be used as the new pivot for dividing the array. 

#### Quick sort algorithm using Lomuto

1. If the low index is less than high index we need to perform the following steps recursively. 
2. Find a new pivot using Lomuto's partitioning. 
3. Sort the left array recursively 
4. Sort the right array recursivly. 
5. Since Quick sort is done in place the algorithm is done when low index is no longer less than high. 


```swift 
func lomutoPartition(_ arr: inout [Int], low: Int, high: Int) -> Int {
  var index = low
  let pivot = arr[high]
  for j in low..<high {
    if arr[j] <= pivot {
      arr.swapAt(index, j)
      index += 1
    }
  }
  arr.swapAt(index, high)
  return index
}

func quickSort(_ arr: inout [Int], low: Int, high: Int) {
  if low < high {
    let pivot = lomutoPartition(&arr, low: low, high: high)
    quickSort(&arr, low: low, high: pivot - 1)
    quickSort(&arr, low: pivot + 1, high: high)
  }
}

var unsortedArr = [10, 80, 10, -9, 0, -11, 13]
quickSort(&unsortedArr, low: 0, high: unsortedArr.count - 1)
print(unsortedArr) // [-11, -9, 0, 10, 10, 13, 80]
```
