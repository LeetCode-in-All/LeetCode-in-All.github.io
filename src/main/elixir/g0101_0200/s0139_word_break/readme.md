[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". 

Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```elixir
defmodule Solution do
  @spec word_break(s :: String.t, word_dict :: [String.t]) :: boolean
  def word_break(s, word_dict) do
    Task.async(fn ->
      breakable?(s, 0, Enum.map(word_dict, &{&1, byte_size(&1)}))
    end)
    |> Task.await()
  end

  defp breakable?("", _idx, _words), do: true

  defp breakable?(s, idx, words) do
    memoized(idx, fn ->
      Enum.any?(words, fn {word, len} ->
        case s do
          <<^word::binary-size(len), rest::binary>> ->
            breakable?(rest, idx + len, words)

          _ ->
            false
        end
      end)
    end)
  end

  defp memoized(key, fun) do
    with nil <- Process.get(key) do
      fun.() |> tap(&Process.put(key, &1))
    end
  end
end
```