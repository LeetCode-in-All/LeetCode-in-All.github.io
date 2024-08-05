[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 20\. Valid Parentheses

Easy

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1.  Open brackets must be closed by the same type of brackets.
2.  Open brackets must be closed in the correct order.

**Example 1:**

**Input:** s = "()"

**Output:** true

**Example 2:**

**Input:** s = "()[]{}"

**Output:** true

**Example 3:**

**Input:** s = "(]"

**Output:** false

**Example 4:**

**Input:** s = "([)]"

**Output:** false

**Example 5:**

**Input:** s = "{[]}"

**Output:** true

**Constraints:**

*   <code>1 <= s.length <= 10<sup>4</sup></code>
*   `s` consists of parentheses only `'()[]{}'`.

## Solution

```elixir
defmodule Solution do

  @compliments %{
      ")" => "(",
      "]" => "[",
      "}" => "{"
  }

  @spec is_valid(s :: String.t) :: boolean
  def is_valid(s) do
    s
    # charlists are easy
    |> String.graphemes()
    # rly gross reduce, but it is a functional way to carry our stack along.
    |> List.foldl([], fn item, acc -> 
         case Map.get(@compliments, item) do
            # Not a closer, just add it to the stack
            nil -> [item | acc]
            # Closer of some kind - check if the top of the stack is 
            # the compliment - if not, add it to the stack.
            # If it is, we can drop one from the stack to clear that set.
            c -> if c == List.first(acc) do
                Enum.drop(acc, 1)
            else 
                [item | acc]
            end
         end
       end)
    # If the stack is empty, then it's valid. Else, we'll
    # have some junk left over from the mismatched pairs.
    |> Enum.empty?()
  end
end
```