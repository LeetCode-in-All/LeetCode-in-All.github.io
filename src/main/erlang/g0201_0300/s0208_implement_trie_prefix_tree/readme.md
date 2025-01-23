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

```erlang
% Initialize the trie using ETS
-spec trie_init_() -> any().
trie_init_() ->
    % Create ETS table if it doesn't exist
    case ets:info(trie_table) of
        undefined ->
            ets:new(trie_table, [set, public, named_table]);
        _ ->
            ets:delete(trie_table),
            ets:new(trie_table, [set, public, named_table])
    end.

% Insert a word into the trie
-spec trie_insert(Word :: unicode:unicode_binary()) -> any().
trie_insert(Word) ->
    % Insert all prefixes with false flag
    insert_prefixes(Word),
    % Mark the complete word with true flag
    ets:insert(trie_table, {Word, true}).

% Search for a complete word
-spec trie_search(Word :: unicode:unicode_binary()) -> boolean().
trie_search(Word) ->
    case ets:lookup(trie_table, Word) of
        [{_, true}] -> true;
        _ -> false
    end.

% Check if any word starts with the given prefix
-spec trie_starts_with(Prefix :: unicode:unicode_binary()) -> boolean().
trie_starts_with(Prefix) ->
    case ets:lookup(trie_table, Prefix) of
        [{_, _}] -> true;
        [] -> false
    end.

% Helper function to insert all prefixes of a word
-spec insert_prefixes(Word :: unicode:unicode_binary()) -> ok.
insert_prefixes(Word) ->
    Prefixes = get_all_prefixes(Word),
    [ets:insert_new(trie_table, {Prefix, false}) || Prefix <- Prefixes],`
    ok.

% Helper function to generate all prefixes of a word
-spec get_all_prefixes(Word :: unicode:unicode_binary()) -> [unicode:unicode_binary()].
get_all_prefixes(Word) ->
    Size = byte_size(Word),
    [binary:part(Word, 0, Len) || Len <- lists:seq(1, Size - 1)].

%% Your functions will be called as such:
%% trie_init_(),
%% trie_insert(Word),
%% Param_2 = trie_search(Word),
%% Param_3 = trie_starts_with(Prefix),

%% trie_init_ will be called before every test case, in which you can do some necessary initializations.
```