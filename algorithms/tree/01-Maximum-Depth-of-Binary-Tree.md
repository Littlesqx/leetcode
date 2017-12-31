## Maximum Depth of Binary Tree

> Given a binary tree, find its maximum depth.
> 
> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
  
**解法一：**

传递level参数记录当前最大层数。题目给出的函数只有根节点参数，所以需要多写一个辅助函数。

```go
func maxDepth(root *TreeNode) int {
    return _maxDepth(root, 0)
}
func _maxDepth(root *TreeNode, level int) int {
    if root == nil {
        return level
    }
    
    left := _maxDepth(root.Left, level+1)
    right := _maxDepth(root.Right, level+1)

    if left > right {
        return left
    }

    return right
}
```

**解法二：**

从叶子节点往回数。

```go
func maxDepth(root *TreeNode) int {
    if root == nil {
        return 0
    }

    left := maxDepth(root.Left)
    right := maxDepth(root.Right)

    if left > right {
        return left+1
    }

    return right+1
}
```