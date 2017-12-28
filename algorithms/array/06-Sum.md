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

- 根据例子，隐藏了一个条件，每个解法里的元素是从小到大排序。

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

只能用两层循环找出三个元素，可以先控制第一个不变，后两个数的确定可以使用low/high pointer找出来。

```go
func threeSum(nums []int) [][]int {
    var solutions [][]int
    n := len(nums)
    sort.Ints(nums)
    for i := 0; i < n-2; i++ {
        j, k := i+1, n-1
        for j < k {
            if nums[i] + nums[j] + nums[k] == 0 {
                solutions = append(solutions, []int{nums[i], nums[j], nums[k]})
                j++; k--;
                for j < k && nums[j] == nums[j-1] {
                    j++
                }
                for j < k && nums[k] == nums[k+1] {
                    k--
                }
            } else if nums[i] + nums[j] + nums[k] < 0 {
                j++
            } else {
                k--
            }
        }
        for i < n-2 && nums[i] == nums[i+1] {
            i++
        }
    }
    return solutions
}
```

## 3Sum Closest
> Given an array S of n integers, 
find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
> For example, given array S = {-1 2 1 -4}, and target = 1.
>
> The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

**关键：**
- Return the sum of the three integers.
 
- You may assume that each input would have exactly one solution.

- 和上一道类似

**解法：**

```go
func getAbs(num int) int {
    if num > 0 {
        return num
    }
    return -num
}

func threeSumClosest(nums []int, target int) int {
    sort.Ints(nums)
    var solutions int = nums[0]+nums[1]+nums[2]
    n, distance := len(nums), getAbs(solutions-target)
    for i := 0; i < n; i++ {
        j, k := i+1, n-1
        for j < k {
            val := nums[i]+nums[j]+nums[k]
            if val == target {
                return val
            } else {
                temp := getAbs(val - target)
                if temp < distance {
                    distance = temp
                    solutions = val
                }
            } 
            if val < target {
                j++
            } else {
                k--
            }
        }
    }
    return solutions
}
```

## 4Sum

> Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
>  
> Note: The solution set must not contain duplicate quadruplets.
>  
> For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.
> A solution set is:

```go
  [
    [-1,  0, 0, 1],
    [-2, -1, 1, 2],
    [-2,  0, 0, 2]
  ]
```
**和前面类似**

**解法：**

```go
func fourSum(nums []int, target int) [][]int {
    var solutions [][]int
    n := len(nums)
    sort.Ints(nums)
    for i := 0; i < n-3; i++ {
        for j := i+1; j < n-2; j++ {
            k, l := j+1, n-1
            for k < l {
                sum := nums[i]+nums[j]+nums[k]+nums[l]
                if sum == target {
                    solutions = append(solutions, []int{nums[i], nums[j], nums[k], nums[l]})
                    k++; l--;
                    for k < l && nums[k] == nums[k-1] {
                        k++
                    }
                    for k < l && nums[l] == nums[l+1] {
                        l--
                    }
                } else if sum < target {
                    k++
                } else {
                    l--
                }
            }
            for j < n-2 && nums[j] == nums[j+1] {
                j++
            }
        }
        for i < n-3 && nums[i] == nums[i+1] {
            i++
        }
    }
    return solutions
}
```

