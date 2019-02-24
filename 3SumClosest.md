Problem from Leetcode:

Description: Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Ruby solution:
````
# @param {Integer[]} nums
# @param {Integer} target
# @return {Integer}
def three_sum_closest(nums, target)
    nums.sort!.each_with_index.inject(1.0 / 0) do |closest_sum, element|
        n, i = element
        closest_sum_tmp = two_sum_closest(nums, n, target, i + 1)
        return closest_sum_tmp if closest_sum_tmp == target
        if (closest_sum - target).abs > (closest_sum_tmp - target).abs
            closest_sum_tmp
        else
            closest_sum
        end
    end
end

def two_sum_closest(nums, n, target, start)
    closest_sum = 1.0 / 0
    i, j = start, nums.count - 1
    range = (start..nums.count)
    while i < j && range === i && range === j
        closest_sum_tmp = n + nums[i] + nums[j]
        return closest_sum_tmp if closest_sum_tmp == target
        if (closest_sum_tmp - target).abs < (closest_sum - target).abs
            closest_sum = closest_sum_tmp
        end
        i += 1 if closest_sum_tmp < target
        j -= 1 if closest_sum_tmp > target
    end
    closest_sum
end
