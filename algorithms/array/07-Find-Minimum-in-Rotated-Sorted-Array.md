## Find Minimum in Rotated Sorted Array

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.
  (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).+
> 
> Find the minimum element.
  You may assume no duplicate exists in the array.
  
  
**关键**

- You may assume no duplicate exists in the array.

**二分法**
可以先排序再选第一个，但效率没有二分法高。

里面有一个规律，因为旋转点只有一个，排好序的数组变成了两段（也是分别排好序的）。

二分，如果数组第一个元素比中间元素大，那么最小值必然存在第一份（包括中间元素）；

反之，最小值存在于第二份（不包括中间元素）。

算法结束标志，当前数组为有序（只需满足首元素小于尾元素），或者当前数组只有一个元素了。

这时候数组第一个元素就是最小值。

```go
func findMin(nums []int) int {
    n := len(nums)
    if n <= 1 {
        return nums[0]
    }
    start, end, min := 0, n - 1, 0
    for start < end {
        if (nums[start] < nums[end]) {
            return nums[start]
        }
        min = (start + end) / 2
        if (nums[start] > nums[min]) {
            end = min
        } else {
            start = min + 1
        }
    }
    return nums[start]
}
```

## Find Minimum in Rotated Sorted Array II

> Follow up for "Find Minimum in Rotated Sorted Array":
  What if duplicates are allowed?
> 
> Would this affect the run-time complexity? How and why?
  Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
>  
> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
>
> Find the minimum element.
>
> The array may contain duplicates.

**跟上题相比，区别在于元素可能有重复：**

稍微改动一下，假如中间元素等于首元素，跳过该首元素即可。

```go
func findMin(nums []int) int {
    n := len(nums)
    if n <= 1 {
        return nums[0]
    }
    start, end, min := 0, n - 1, 0
    for start < end {
        if (nums[start] < nums[end]) {
            return nums[start]
        }
        min = (start + end) / 2
        if (nums[start] > nums[min]) {
            end = min
        } else if (nums[start] < nums[min]) {
            start = min + 1
        } else {
            start = start + 1
        }
    }
    return nums[start]
}
```