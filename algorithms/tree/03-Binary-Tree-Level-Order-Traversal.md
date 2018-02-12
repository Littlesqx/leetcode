## Binary Tree Level Order Traversal
```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```

**考的是广度优先搜索**

第一种办法就是用栈的方式遍历

```go
func levelOrder(root *TreeNode) [][]int {
    if root == nil {
        return nil
    }
    solutions := [][]int{}
    queue := []*TreeNode{ root }
    for len(queue) > 0 {
        current, length := []int{}, len(queue)
        for i:=0; i<length; i++ {
            temp := queue[0]
            current = append(current, temp.Val)
            queue = queue[1:len(queue)] // pop
            if temp.Left != nil {
                queue = append(queue, temp.Left) // push
            }
            if temp.Right != nil {
                queue = append(queue, temp.Right) // push
            }
        }
        solutions = append(solutions, current)
    }
    return solutions
}
```

第二种方法其实用了深度优先搜索，数组可以 index (层级) 动态修改

```go
func levelOrder(root *TreeNode) [][]int {
    solutions := [][]int{}
    var updateSolutions func(*TreeNode, int)
    updateSolutions = func(parent *TreeNode, level int) {
        if parent == nil {
          return
        }
        if(level > len(solutions)-1) {
            solutions = append(solutions, []int{})
        }
        solutions[level] = append(solutions[level], parent.Val)
        updateSolutions(parent.Left, level+1)
        updateSolutions(parent.Right, level+1)
    }
    updateSolutions(root, 0)
    return solutions
}
```

## Binary Tree Level Order Traversal II
   
```
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
```

对比前面的，反转一下就好。

广度优先搜索：

```go
func levelOrderBottom(root *TreeNode) [][]int {
    if root == nil {
        return nil
    }
    solutions := [][]int{}
    queue := []*TreeNode{ root }
    for len(queue) > 0 {
        current, length := []int{}, len(queue)
        for i:=0; i<length; i++ {
            temp := queue[0]
            current = append(current, temp.Val)
            queue = queue[1:len(queue)] // pop
            if temp.Left != nil {
                queue = append(queue, temp.Left) // push
            }
            if temp.Right != nil {
                queue = append(queue, temp.Right) // push
            }
        }
        solutions = append([][]int{ current }, solutions...)
    }
    return solutions
}
```

深度优先搜索：

```go
func levelOrderBottom(root *TreeNode) [][]int {
    solutions := [][]int{}
    var updateSolutions func(*TreeNode, int)
    updateSolutions = func(parent *TreeNode, level int) {
        if parent == nil {
          return
        }
        if(level > len(solutions)-1) {
            solutions = append([][]int{ []int{} }, solutions...)
        }
        solutions[len(solutions)-level-1] = append(solutions[len(solutions)-level-1], parent.Val)
        updateSolutions(parent.Left, level+1)
        updateSolutions(parent.Right, level+1)
    }
    updateSolutions(root, 0)
    return solutions
}
```

## Binary Tree Zigzag Level Order Traversal
   
```
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
  [15,7]
]
```

由第一道变形，基数行不反转，偶数行反转。。。

广度优先搜索：

```go
func zigzagLevelOrder(root *TreeNode) [][]int {
    if root == nil {
        return nil
    }
    solutions := [][]int{}
    queue := []*TreeNode{ root }
    for len(queue) > 0 {
        current, length := []int{}, len(queue)
        for i:=0; i<length; i++ {
            temp := queue[0]
            current = append(current, temp.Val)
            queue = queue[1:len(queue)] // pop
            if temp.Left != nil {
                queue = append(queue, temp.Left) // push
            }
            if temp.Right != nil {
                queue = append(queue, temp.Right) // push
            }
        }
        solutions = append(solutions, current)
    }
    for i:=1; i<len(solutions); i=i+2 {
        for left, right := 0, len(solutions[i])-1; left < right; left, right = left+1, right-1 {
            solutions[i][left], solutions[i][right] = solutions[i][right], solutions[i][left]
        }
    }
    return solutions
}
```

后面的反转步骤可以再优化，比如：

```go
func zigzagLevelOrder(root *TreeNode) [][]int {
    solutions := [][]int{}
    var updateSolutions func(*TreeNode, int)
    updateSolutions = func(parent *TreeNode, level int) {
        if parent == nil {
          return
        }
        if(level > len(solutions)-1) {
            solutions = append(solutions, []int{})
        }
        if level%2 == 1 {
            solutions[level] = append([]int{ parent.Val }, solutions[level]...)
        } else {
            solutions[level] = append(solutions[level], parent.Val)  
        }
       
        updateSolutions(parent.Left, level+1)
        updateSolutions(parent.Right, level+1)
    }
    updateSolutions(root, 0)
    return solutions
}
```

