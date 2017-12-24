## Merge Sorted Array
> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
>  
> Note:
>
> You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

**解法：**

```Go
func merge(nums1 []int, m int, nums2 []int, n int)  {
    total, i, j := m+n-1, m-1, n-1
    for total >= 0 {
    	if i >= 0 && j >= 0{
    		if nums1[i] > nums2[j] {
    			nums1[total] = nums1[i]
    			i--
    		} else {
    			nums1[total] = nums2[j]
    			j--
    		}
    	} else if i >= 0 {
    		nums1[total] = nums1[i]
    		i--
    	} else if j >= 0 {
    		nums1[total] = nums2[j]
    		j--
    	}
    	total--
    }
}
```