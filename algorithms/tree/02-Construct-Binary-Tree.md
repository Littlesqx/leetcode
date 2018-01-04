
如有如下的二叉树：

```
                1
        --------|-------
        2               3
    ----|----       ----|----
    4       5       6       7
```

前序遍历： 1245347

中序遍历： 4251637

后序遍历： 4526731

且知道一颗二叉树的前/后序遍历和中序遍历，可以还原该树；只知道前序遍历和后序遍历，不能还原。

- 知道前序遍历+中序遍历

  - 前序遍历的第一个元素为根节点，以该元素划分中序遍历为两部分元素，分别就是对应父亲节点的左右子树。

- 知道后序遍历+中序遍历

  - 后序遍历的最后一个元素为根节点，以该元素划分中序遍历为两部分，分别就是对应父亲节点的左右子树。

- 这两种情况下，左右子树元素在两种遍历都是连续的，只是顺序不一样。例如1的左子树，在中序遍历是425，而在前序和后序遍历分别是245和452。

## from Preorder and Inorder Traversal

> Given preorder and inorder traversal of a tree, construct the binary tree.+

**解法**

```go
func buildTree(preorder []int, inorder []int) *TreeNode {
    m := map[int]int{}
    for i := range inorder {
        m[inorder[i]] = i
    }
    return _buildTree(preorder, 0, len(preorder)-1, inorder, 0, len(inorder)-1, m)
}

func _buildTree(preorder []int, preL int, preR int, inorder []int, inL int, inR int, m map[int]int) *TreeNode {
    
    if preL > preR || inL > inR {
        return nil
    }

    min := m[preorder[preL]]
    num := min-inL
    root := &TreeNode{ Val: preorder[preL] }

    root.Left = _buildTree(preorder, preL+1, preL+num, inorder, inL, min-1, m)
    root.Right = _buildTree(preorder, preL+num+1, preR, inorder, min+1, inR, m)

    return root
}
```

## from Inorder and Postorder Traversal

> Given inorder and postorder traversal of a tree, construct the binary tree.
  
**解法**

```go
func buildTree(inorder []int, postorder []int) *TreeNode {
    m := map[int]int{}
    for i := range inorder {
        m[inorder[i]] = i
    }
    return _buildTree(postorder, 0, len(postorder)-1, inorder, 0, len(inorder)-1, m)
}

func _buildTree(postorder []int, postL int, postR int, inorder []int, inL int, inR int, m map[int]int) *TreeNode {
    
    if postL > postR || inL > inR {
        return nil
    }

    min := m[postorder[postR]]
    num := min-inL
    root := &TreeNode{ Val: postorder[postR] }

    root.Left = _buildTree(postorder, postL, postL+num-1, inorder, inL, min-1, m)
    root.Right = _buildTree(postorder, postL+num, postR-1, inorder, min+1, inR, m)

    return root
}

```