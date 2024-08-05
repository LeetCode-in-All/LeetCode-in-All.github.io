[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 10\. Regular Expression Matching

Hard

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

*   `'.'` Matches any single character.
*   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

**Example 1:**

**Input:** s = "aa", p = "a"

**Output:** false

**Explanation:** "a" does not match the entire string "aa". 

**Example 2:**

**Input:** s = "aa", p = "a\*"

**Output:** true

**Explanation:** '\*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa". 

**Example 3:**

**Input:** s = "ab", p = ".\*"

**Output:** true

**Explanation:** ".\*" means "zero or more (\*) of any character (.)". 

**Example 4:**

**Input:** s = "aab", p = "c\*a\*b"

**Output:** true

**Explanation:** c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab". 

**Example 5:**

**Input:** s = "mississippi", p = "mis\*is\*p\*."

**Output:** false 

**Constraints:**

*   `1 <= s.length <= 20`
*   `1 <= p.length <= 30`
*   `s` contains only lowercase English letters.
*   `p` contains only lowercase English letters, `'.'`, and `'*'`.
*   It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

## Solution

```elixir
defmodule Solution do
  @cache Agent

  @spec is_match(s :: String.t, p :: String.t) :: boolean
  def is_match(s, p) do
    :ets.new(:cache, [:named_table, :set, {:read_concurrency, true}])
    result = is_match(s, p, 0, 0)
    :ets.delete(:cache)
    result
  end

  defp is_match(s, p, i, j) do
    case :ets.lookup(:cache, {i, j}) do
      [{_, result}] -> result
      [] ->
        result = 
          if j == String.length(p) do
            i == String.length(s)
          else
            first_match = i < String.length(s) && (String.at(s, i) == String.at(p, j) || String.at(p, j) == ".")
            if (j + 1) < String.length(p) && String.at(p, j + 1) == "*" do
              (first_match && is_match(s, p, i + 1, j)) || is_match(s, p, i, j + 2)
            else
              first_match && is_match(s, p, i + 1, j + 1)
            end
          end

        :ets.insert(:cache, { {i, j}, result})
        result
    end
  end
end
```