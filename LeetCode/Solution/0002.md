[View my solution on LeetCode](https://leetcode.com/problems/add-two-numbers/solutions/8284024/a-simple-solution-rtl-100-mem-1172-by-jo-a2mj/)

# Intuition

The problem asks us to add two numbers represented by linked lists, where each node contains a single digit, and the digits are stored in reverse order. This reverse order is actually highly advantageous because it mimics how we manually perform addition on paper: we start from the least significant digit (the head of the lists) and move towards the most significant digit, carrying over any overflow to the next column.

# Approach

1. **Initialize a Dummy Head**: We use a dummy node `res(0)` and a pointer `buf` to easily build and traverse the resulting linked list without worrying about edge cases for the head node.
2. **Track the Carry/Remainder**: We use an integer variable `remainder` to store the carry-over from the addition of the previous digits.
3. **Iterate Through the Lists**: We use a `while` loop that continues as long as there is at least one node left to process in `l1` or `l2`, or if there is a remaining `remainder` to be added at the end.
4. **Sum Digits**: Inside the loop, we start the sum (`rst`) with the current `remainder`. If `l1` or `l2` is not null, we add its value to `rst` and advance the respective list pointer.
5. **Create New Node & Update Carry**:
* The digit to store in the current node is `rst % 10`.
* The new carry-over for the next iteration becomes `rst / 10`.


6. **Return the Result**: Finally, we return `res.next`, which skips our initial dummy node and points to the true head of the summed linked list.

# Complexity

* Time complexity:

$$O(\max(m, n))$$



Where $m$ and $n$ represent the lengths of `l1` and `l2` respectively. The algorithm iterates at most $\max(m, n) + 1$ times to process all digits.
* Space complexity:

$$O(\max(m, n))$$



The length of the new linked list is at most $\max(m, n) + 1$, which represents the memory allocated for the output list.

# Code

```cpp []
/**
 * Definition for singly-linked list.
 * struct ListNode {
 * int val;
 * ListNode *next;
 * ListNode() : val(0), next(nullptr) {}
 * ListNode(int x) : val(x), next(nullptr) {}
 * ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode res(0);
        ListNode* buf = &res;
        int remainder = 0;
        int rst = 0;
        while (l1 != nullptr || l2 != nullptr || remainder != 0) {
            rst = remainder;
            if(l1 != nullptr){
                rst+=l1->val;
                l1 = l1->next;
            }
            if(l2 != nullptr){
                rst+=l2->val;
                l2 = l2->next;
            }
            buf->next = new ListNode(rst % 10);
            remainder = rst / 10;
            buf = buf->next;
        }
        return res.next;
    }
};

```