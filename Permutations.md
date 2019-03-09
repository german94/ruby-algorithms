Problem from LeetCode:

Description:

Solution: use an auxiliar recursive method to accumulate the current permutation and the list of all permutations. We add the current permutation to the list when it has all the elements, otherwise we make a recursive call adding an element and removing it from the list of available numbers.

Ruby code:
```
# @param {Integer[]} nums
# @return {Integer[][]}
def permute(nums)
    [].tap { |permutations| generate_permutations(nums, [], permutations) }
end

def generate_permutations(elements, current_permutation, permutations)
    return (permutations << current_permutation) if elements.empty?
    (0..elements.size - 1).each do |i|
        other_elements = elements.reject.with_index { |_, k| k == i }
        generate_permutations(other_elements, current_permutation + [elements[i]], permutations)
    end
end
```
