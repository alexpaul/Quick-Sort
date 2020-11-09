# Quick-Sort

Quick sort algorithm in Swift. 

Quick sorting algorithm uses a divide and conquer approach a bit similar to merge sort. Given an unsorted array and a partitioning mehtod listed below a pivot is calculated. The array is divided.....

## Partitioning methods 

* Naive approach
* Lumoto's Partitioning
* Dutch Flag 


## Quick sort implmentation using Lomuto's Partitioning 

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
