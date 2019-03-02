Problem from LeetCode:

Description: given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Solution: generate valid parenthesis in a depth first search checking:

1. if we have a complete string (we have no more open nor closed parenthesis to use)
2. if all we can do is close parenthesis (we have no more parenthesis to open)
3. if we can open or close parenthesis (this is where we add the combinations)

```
# @param {Integer} n
# @return {String[]}
def generate_parenthesis(n)
    result = []
    generate_parenthesis_aux(n, n, "", result)
    result
end

def generate_parenthesis_aux(open, closed, sub_solution, result)
    return result << sub_solution if open == 0 && closed == 0
    return result << sub_solution + ')'*closed if open == 0
    if open > 0
        generate_parenthesis_aux(open - 1, closed, sub_solution + '(', result)
    end
    if open < closed
        generate_parenthesis_aux(open, closed - 1, sub_solution + ')', result)
    end
end
```
