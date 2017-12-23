## Remove Element
> Given an array and a value, remove all instances of that value in-place and return the new length.

> Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

> The order of elements can be changed. It doesn't matter what you leave beyond the new length.

> Example:
> 
> `Given nums = [3,2,2,3], val = 3,Your function should return length = 2, with the first two elements of nums being 2.`

**关键**

- Do not allocate extra space for another array.
- The order of elements can be changed.
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
> 回过头看，slice类型的拼接，似乎额外申请空间了；虽然可以AC，但违规了，空间复杂度应该是O(n)。

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
**方法三、从尾部开始获取元素，也是“覆盖”一个新数组。**
```Go
func removeElement(nums []int, val int) int {
	n, i := len(nums), 0
	for i < n {
		if nums[i] == val {
			nums[i] = nums[n-1]
			n--
		} else {
			i++
		}
	}
	return n
}
```



