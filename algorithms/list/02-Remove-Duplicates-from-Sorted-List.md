## Remove Duplicates from Sorted List

> Given a sorted linked list, delete all duplicates such that each element appear only once.
>  
> For example,
> Given 1->1->2, return 1->2.
>
> Given 1->1->2->3->3, return 1->2->3.

**解法**

```go
func deleteDuplicates(head *ListNode) *ListNode {
    p := head
    for p != nil && p.Next != nil {
        if p.Val != p.Next.Val {
            p = p.Next
        } else {
            p.Next = p.Next.Next
        }
    }
    return head
}
```

## Remove Duplicates from Sorted List II

> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.
> 
> For example,
> Given 1->2->3->3->4->4->5, return 1->2->5.
>
> Given 1->1->1->2->3, return 2->3.

pre 节点存上一个节点地址，初始值用了一个临时的节点 temp ，避免第一个节点就开始重复的情况。

```go
func deleteDuplicates(head *ListNode) *ListNode {
    p, temp := head, &ListNode{ Next: head }
    pre := temp
    for p != nil && p.Next != nil {
        if p.Val != p.Next.Val {
            pre = p
            p = p.Next
        } else {
            n := p.Next.Next
            for n != nil && n.Val == p.Val {
                n = n.Next
            }
            pre.Next = n
            p = n
        }
    }
    return temp.Next
}
```