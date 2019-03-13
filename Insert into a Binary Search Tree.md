Problem from LeetCode

Description: Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

Note that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

Solution: check recursively if the value of the node to insert is greater or lesser than the current root and then walk through the corresponding subtree. The base case is when there is no root node to check the value with, so we create the new node and return it.

Ruby code:
```
# Definition for a binary tree node.
# class TreeNode
#     attr_accessor :val, :left, :right
#     def initialize(val)
#         @val = val
#         @left, @right = nil, nil
#     end
# end

# @param {TreeNode} root
# @param {Integer} val
# @return {TreeNode}
def insert_into_bst(root, val)
    root.tap do |root|
        return TreeNode.new(val) unless root
        if val > root.val
            root.right = insert_into_bst(root.right, val)
        else
            root.left = insert_into_bst(root.left, val)
        end
    end
end
