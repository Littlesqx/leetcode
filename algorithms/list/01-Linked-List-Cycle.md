## Linked List Cycle

> Given a linked list, determine if it has a cycle in it.
> 
> Follow up:
> Can you solve it without using extra space

使用两个指针，一个每次走一步，另一个每次走两步；链表遍历完之前指针重合则存在环。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == NULL || head->next == NULL) {
            return false;
        }
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast->next != NULL && fast->next->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) {
                return true;
            }
        }
        return false;
    }
};
```

## Linked List Cycle II

> Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
> 
> Note: Do not modify the linked list.
> 
> Follow up:
> Can you solve it without using extra space?

在上一道题的基础上找出环的开始节点。其中存在的规律见 [这里](https://siddontang.gitbooks.io/leetcode-solution/content/linked_list/linked_list_cycle.html) 。 

**解法**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (head == NULL || head->next == NULL) {
            return NULL;
        }
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast->next != NULL && fast->next->next != NULL) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) {
                slow = head;
                while(fast != slow) {
                    fast = fast->next;
                    slow = slow->next;
                }
                return slow;
            }
        }
        return NULL;
    }
};
```