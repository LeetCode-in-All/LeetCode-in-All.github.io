[![](https://img.shields.io/github/stars/javadev/LeetCode-in-All?label=Stars&style=flat-square)](https://github.com/javadev/LeetCode-in-All)
[![](https://img.shields.io/github/forks/javadev/LeetCode-in-All?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/javadev/LeetCode-in-All/fork)

## 208\. Implement Trie (Prefix Tree)

Medium

A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

*   `Trie()` Initializes the trie object.
*   `void insert(String word)` Inserts the string `word` into the trie.
*   `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
*   `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.

**Example 1:**

**Input**

    ["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
    [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]

**Output:** [null, null, true, false, true, null, true]

**Explanation:**

    Trie trie = new Trie();
    trie.insert("apple"); trie.search("apple"); // return True
    trie.search("app"); // return False
    trie.startsWith("app"); // return True
    trie.insert("app");
    trie.search("app"); // return True 

**Constraints:**

*   `1 <= word.length, prefix.length <= 2000`
*   `word` and `prefix` consist only of lowercase English letters.
*   At most <code>3 * 10<sup>4</sup></code> calls **in total** will be made to `insert`, `search`, and `startsWith`.

## Solution

```ruby
# @param {String} string
# @return {String}
class Trie
  def initialize
    @root = TrieNode.new
    @start_with = false
  end

=begin
    :type word: String
    :rtype: Void
=end
  def insert(word)
    insert_recursive(word, @root, 0)
  end

=begin
    :type word: String
    :rtype: Boolean
=end
  def search(word)
    search_recursive(word, @root, 0)
  end

=begin
    :type prefix: String
    :rtype: Boolean
=end
  def starts_with(prefix)
    search(prefix)
    @start_with
  end

  private

  class TrieNode
    attr_accessor :children, :is_word

    def initialize
      @children = Array.new(26)
      @is_word = false
    end
  end

  def insert_recursive(word, root, idx)
    if idx == word.length
      root.is_word = true
      return
    end

    index = word[idx].ord - 'a'.ord
    root.children[index] ||= TrieNode.new
    insert_recursive(word, root.children[index], idx + 1)
  end

  def search_recursive(word, root, idx)
    if idx == word.length
      @start_with = true
      return root.is_word
    end

    index = word[idx].ord - 'a'.ord
    if root.children[index].nil?
      @start_with = false
      return false
    end

    search_recursive(word, root.children[index], idx + 1)
  end
end

# Your Trie object will be instantiated and called as such:
# obj = Trie.new()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.starts_with(prefix)
```