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

The Lomuto's algorithm is used to find a new index to use a the pivot when dividing the array in left and right sides. 

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
func lomutoPartitioning(_ arr: inout [Int], _ low: Int, _ high: Int) -> Int {
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

func quickSort(_ arr: inout [Int], _ low: Int, _ high: Int) {
  if low < high {
    let pivot = lomutoPartitioning(&arr, low, high)
    quickSort(&arr, low, pivot - 1)
    quickSort(&arr, pivot + 1, high)
  }
}

var unsortedArr = [68, 46, 91, 42, -37, 50, 52]
quickSort(&unsortedArr, 0, unsortedArr.count - 1)
print(unsortedArr) // [-37, 42, 46, 50, 52, 68, 91]
```

## Resources 

1. [Wikipedia - Quicksort](https://en.wikipedia.org/wiki/Quicksort)
1. [RW - Swift Algorithm Club](https://github.com/raywenderlich/swift-algorithm-club/tree/master/Quicksort)
