Problem from LeetCode:

Description: S and T are strings composed of lowercase letters. In S, no letter occurs more than once.

S was sorted in some custom order previously. We want to permute the characters of T so that they match the order that S was sorted. More specifically, if x occurs before y in S, then x should occur before y in the returned string.

Return any permutation of T (as a string) that satisfies this property.

Solution: basically we use a hash to map each character to its corresponding index in s, this is what will let us to sort the final string later. Then we map the string t converting each character to a tuple, containing the character and the order of that character according to the previously created hash. We then sort the list using the second component of each tuple and then discard the second elements of the tuples and join the first ones to create the final string.

Ruby code:
```
# @param {String} s
# @param {String} t
# @return {String}
def custom_sort_string(s, t)
    s.split('').each_with_index.with_object({}) { |(c, i), char_order| char_order[c] = i }.tap do |order|
    return t.split('').map { |e| [e, order[e] || t.size] }.sort_by { |e| e[1] }.map { |e| e[0] }.join
    end
end
```
