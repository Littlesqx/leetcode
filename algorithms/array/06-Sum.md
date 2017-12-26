## Two Sum

> Given an array of integers, return indices of the two numbers such that they add up to a specific target.
> 
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
> 
> Example:
>
> Given nums = [2, 7, 11, 15], target = 9,
  ```
  Because nums[0] + nums[1] = 2 + 7 = 9,
  return [0, 1].
  ```
**关键**

- 假定只有一种组合符合要求

- 不能使用相同元素

**解法一： 两个for循环**
```go
func twoSum(nums []int, target int) []int {
    n := len(nums)
    for i := 0; i < n; i++ {
        for j := i+1; j < n; j++ {
            if check := nums[i]+nums[j]; check == target {
                return []int{i, j}
            }
        }
    }
    return nil
}
```

虽然可以AC，但该算法时间复杂度为`O(n^2)`，速度是比较慢的。

可以利用map类型巧妙优化，即利用map的key存值。

**解法二：利用map类型**

```go
func twoSum(nums []int, target int) []int {
    m, n := make(map[int]int), len(nums)
    for i := 0; i < n; i++ {
        another := target - nums[i]
        if j, check := m[another]; check {
            return []int{j, i}
        }
        m[nums[i]] = i
    }
    return nil
}
```

> 两个返回值的方式可以检查map是否存在目标键值对，
例如 `value, check := m['test']`，返回的`value`是键`test`对应的值，
`check`是一个bool值，表示是否存在`test`对应的键值对。

优化后可以看到时间复杂度为`O(n)`。


## 3Sum

> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? 
Find all unique triplets in the array which gives the sum of zero.
>  
> Note: The solution set must not contain duplicate triplets.
>  
> For example, given array S = [-1, 0, 1, 2, -1, -4],
> 
> A solution set is: 

```go
  [
    [-1, 0, 1],
    [-1, -1, 2]
  ]
```

**关键**

- must not contain duplicate triplets

- 根据例子，隐藏了一个条件，每个解法里的元素是从小到大排序的，
这些元素不可重复（数组下标一样才算重复）。

**方法一、暴力法**

```go
func isExist(nums [][]int, a int, b int) bool {
    if len(nums) > 0 {
        for i := len(nums)-1; i >= 0; i-- {
            if nums[i][0] == a && nums[i][1] == b {
                return true
            } else if nums[i][0] < a {
                return false
            }
        }
    }
    return false
}

func threeSum(nums []int) [][]int {
    sort.Ints(nums)
    var solutions [][]int
    n := len(nums)
    for i := 0; i < n-2; i++ {
        for j := i+1; j < n-1; j++ {
            for k := j+1; k < n; k++ {
                if nums[i] + nums[j] + nums[k] == 0 {
                    if flag := isExist(solutions, nums[i], nums[j]); flag {
                        continue
                    }
                    solutions = append(solutions, []int{nums[i], nums[j], nums[k]})
                }
            }
        }
    }
    return solutions
}
```

然而超时了。。。看来O(n^3)的时间复杂度是不可行的。

