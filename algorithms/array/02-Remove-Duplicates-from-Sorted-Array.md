## Remove Element
> Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.
>
> Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

> Example:

> `Given nums = [1,1,2],Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.`

**关键**

- a sorted array
- Do not allocate extra space for another array
- It doesn't matter what you leave beyond the new length

**方法一、利用原本数组空间重新“覆盖”一个新数组。**
```Go
func removeDuplicates(nums []int) int {
	j, n := 0, len(nums)
	for i := 1; i < n; i++ {
		if nums[j] != nums[i] {
			j++
			nums[j] = nums[i]
		}
	}
	if n == 0 {
		return 0
	}
	return j+1
}
```