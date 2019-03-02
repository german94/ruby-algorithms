Problem from LeetCode:

Description: Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers. 
If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
The replacement must be in-place and use only constant extra memory.

Solution: iterate the array from the last element to the first, saving the maximum value until we find an element lesser than the current max. Once we found that element, we'll call it n, we swap it with the smallest element that appears after n. Then we sort in ascending order the sub-array starting from the element next to n to the last element. The sorting is needed because if we just swap the elements we can have a greater permutation but no the exactly next permutation.

Ruby code:
```
# @param {Integer[]} nums
# @return {Void} Do not return anything, modify nums in-place instead.
def next_permutation(nums)
    max = nums[-1]
    index_to_swap = nil
    (0..nums.count - 1).reverse_each do |i|
        if nums[i] < max
            index_to_swap = i
            break
        end
        max = nums[i]
    end
    return nums.sort! unless index_to_swap
    index, val = nil, 1.0 / 0
    (index_to_swap + 1..nums.count - 1).each do |i|
        if nums[i] > nums[index_to_swap] && nums[i] < val
            index, val = i, nums[i]
        end
    end
    nums[index_to_swap], nums[index] = nums[index], nums[index_to_swap]
    nums[index_to_swap + 1..-1] = nums[index_to_swap + 1..-1].sort
end
```

Note: the deascription says that the algorithm cannot use extra memory. If you look carefully this algorithm uses extra memory because ```nums[index_to_swap + 1..-1]``` creates a copy of the sub-array. However, this is not a big deal because we could just sort the array in place (we would need to implement a sorting algorithm because Ruby does not have methods for sorting sub-arrays in place).
