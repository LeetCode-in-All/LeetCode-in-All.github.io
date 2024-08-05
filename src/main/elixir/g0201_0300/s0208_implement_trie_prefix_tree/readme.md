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

**Input** ["Trie", "insert", "search", "search", "startsWith", "insert", "search"] [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]

**Output:** [null, null, true, false, true, null, true]

**Explanation:** 

Trie trie = new Trie(); 

trie.insert("apple"); 

trie.search("apple"); // return True 

trie.search("app"); // return False 

trie.startsWith("app"); // return True 

trie.insert("app"); 

trie.search("app"); // return True

**Constraints:**

*   `1 <= word.length, prefix.length <= 2000`
*   `word` and `prefix` consist only of lowercase English letters.
*   At most <code>3 * 10<sup>4</sup></code> calls **in total** will be made to `insert`, `search`, and `startsWith`.

## Solution

```elixir
defmodule Trie do
  use GenServer

  @spec init_() :: any
  def init_() do
    GenServer.start_link(__MODULE__, nil, name: __MODULE__)
    GenServer.call(__MODULE__, :start)
  end

  @spec insert(word :: String.t) :: any
  def insert(word) do
    GenServer.call(__MODULE__, {:insert, word})
  end

  @spec search(word :: String.t) :: boolean
  def search(word) do
    GenServer.call(__MODULE__, {:search, word})
  end

  @spec starts_with(prefix :: String.t) :: boolean
  def starts_with(prefix) do
    GenServer.call(__MODULE__, {:prefix, prefix})
  end

  @impl true
  def init(_) do
    {:ok, nil}
  end

  @impl true
  def handle_call(:start, _, _) do
    {:reply, nil, Map.new()}
  end

  def handle_call({:insert, word}, _, map) do
    String.codepoints(word)
    |> Enum.reduce({map, ""}, fn ch, {map, prefix} ->
      {Map.put_new(map, prefix, false), prefix <> ch}
    end)
    |> elem(0)
    |> Map.put(word, true)
    |> then(fn map -> {:reply, nil, map} end)
  end

  def handle_call({:search, word}, _, map) do
    {:reply, Map.get(map, word, false), map}
  end

  def handle_call({:prefix, prefix}, _, map) do
    {:reply, Map.get(map, prefix) != nil, map}
  end
end
```