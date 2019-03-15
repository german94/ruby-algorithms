Problem from LeetCode:

Description:

Solution: we have to check if there is a bijective mapping between the pattern and each word of the list, so we can use two hashes to construct the function. If a string has not the same length than the pattern we know for sure that does not exist such a bijective function. We can then iterate both of the strings and check, for each character, if there exists a mapping for that character and if the mapping satisfies the current iteration (if not, then we return false). If the mapping does not exist, then we create it.

```
# @param {String[]} words
# @param {String} pattern
# @return {String[]}
def find_and_replace_pattern(words, pattern)
    words.select { |word| word.size == pattern.size && matches_pattern?(word, pattern) }
end

def matches_pattern?(word, pattern)
    word.split('').each_with_index.with_object({ from_word: {}, from_pattern: {}}) do |(c, i), letters_mapping|
        unless letters_mapping[:from_word][c]
            return false if letters_mapping[:from_pattern][pattern[i]]
            letters_mapping[:from_word][c] = pattern[i]
            letters_mapping[:from_pattern][pattern[i]] = c
        end
        return false if letters_mapping[:from_word][c] != pattern[i]
    end
end
```
