## Remove Element
> Given an array and a value, remove all instances of that value in-place and return the new length.

> Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

> The order of elements can be changed. It doesn't matter what you leave beyond the new length.

> Example:
> 
> `Given nums = [3,2,2,3], val = 3,Your function should return length = 2, with the first two elements of nums being 2.`

**关键**

- Do not allocate extra space for another array.

- It doesn't matter what you leave beyond the new length.

**方法一、直接去掉元素，前后两部分重新拼接。**
```Go
func removeElement(nums []int, val int) int {
	n := len(nums)
    for i := 0; i < n; i++ {
    	if val == nums[i] {
    		nums = append(nums[:i], nums[i+1:]...)
    		i--
    	}
    }
    return len(nums)
}
```
**方法二、利用原本数组空间重新“覆盖”一个新数组。**
```Go
func removeElement(nums []int, val int) int {
	j, n := 0, len(nums)
    for i := 0; i < n; i++ {
    	if val != nums[i] {
    		nums[j] = nums[i]
    		j++
    	}
    }
    return j
}
```
严格来说，移除数组元素，那原本数组的长度和元素位置应该都变化。比如：[1,2,2,3] 移除2后应该是 [1,3]。
而方法二的结果是[1,3,2,3]。但是题目说了，不考虑返回length后的多余元素。



