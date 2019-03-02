Problem from LeetCode:

Description: Given a linked list, swap every two adjacent nodes and return its head. You may not modify the values in the list's nodes, only nodes itself may be changed.

Solution: swap de first two nodes and the resulting second node need to point to the swapped sublist

Ruby code:
```
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val)
#         @val = val
#         @next = nil
#     end
# end

# @param {ListNode} head
# @return {ListNode}
def swap_pairs(head)
    return head unless (head && head.next)
    sub_list_head = head.next.next
    new_head = head.next # head = 2
    new_head.next = head # 2 -> 1
    head.next = swap_pairs(sub_list_head)
    new_head
end
