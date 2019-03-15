Problem from LeetCode

Description: Given two strings representing two complex numbers.

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.

Notes:
 - The input strings will not have extra blank.
 - The input strings will be given in the form of a+bi, where the integer a and b will both belong to the range of [-100, 100]. And the output should be also in this form.

Solution: this is a really simple problem that requires only basic mathematical skills to apply the distributive property and treat with the real terms on one side and the imaginary ones on the other. The way I solved this problem in order to avoid code repetition while keeping it simple, was using lambdas to extract the real and imaginary terms. It could be solved defining methods extract_a and extract_b but the logic of this methods is really simple and there is only one method that needs them, so lambdas are a very good choice. Once we have extracted the terms and applied the distributive property, the only thing to do is a little string interpolation in order to return the result.

```
# @param {String} a
# @param {String} b
# @return {String}
def complex_number_multiply(a, b)
    extract_a = lambda { |complex_number| complex_number.split('+')[0].to_i }
    extract_b = lambda { |complex_number| complex_number.split('+')[1].split('i')[0] .to_i }
    first_number = { a: extract_a[a], b: extract_b[a] }
    second_number = { a: extract_a[b], b: extract_b[b] }
    a = first_number[:a] * second_number[:a] - first_number[:b] * second_number[:b]
    b = second_number[:a] * first_number[:b] + second_number[:b] * first_number[:a]
    "#{a}+#{b}i"
end
```
