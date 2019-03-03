Problem from LeetCode:

Description: given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

First solution: this solution requires sorting the array and using a two pointers technique. We start with one pointer at the first element and the other at the last, then for each iteration we return the indices of the pointers if the corresponding elements add up to the target. Otherwise, we check if the sum is grater than the target, in that case we decrease the second pointer, if it's lesser than the target we increase the first pointer. This loop is O(n), but the sorting requires O(n.log(n)) so the complexity of this algorithm is O(n.log(n)). The memory usage is O(1) (except for the each_with_index that creates a new array but it could be avoided) because we don't need extra memory, just iterate the array.

Ruby code:
```
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer[]}
def two_sum(nums, target)
    nums = nums.each_with_index.map { |v, i| { value: v, index: i } }.sort_by! { |e| e[:value] }
    i, j = 0, nums.count - 1
    while i < j
        sum = nums[i][:value] + nums[j][:value]
        return nums[i][:index], nums[j][:index] if sum == target
        if sum > target
            j -= 1
        else
            i += 1
        end
    end
end
```

Second solution: using extra memory we can iterate the array and store what elements we visited. For each element n then, we can check if we've visited target - n, in that case we found the solution and return both indices. Otherwise, we mark the element as visited. This solution has O(n) temporal complexity becuase accessing an element of the hash is O(1) (in average, because this complexity decreases as the number of buckets increases) but we need O(n) memory.

Ruby code:
```
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer[]}
def two_sum(nums, target)
    nums.each_with_index.each_with_object({}) do |(n, i), hash|
        return i, hash[target - n] if hash[target - n]
        hash[n] = i
    end
end
```
