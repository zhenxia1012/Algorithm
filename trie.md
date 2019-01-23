# Trie

```java
class Trie {
    TrieNode root;
    
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode cur = root;
        for (char c : word.toCharArray()) {
            if (cur.dict[c - 'a'] == null) 
                cur.dict[c - 'a'] = new TrieNode();
            cur = cur.dict[c - 'a'];
            cur.count++;
        }
        cur.word = word;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode cur = root;
        for (char c : word.toCharArray()) {
            if (cur.dict[c - 'a'] == null) 
                return false;
            cur = cur.dict[c - 'a'];
        }
        return cur.word != null;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode cur = root;
        for (char c : prefix.toCharArray()) {
            if (cur.dict[c - 'a'] == null) 
                return false;
            cur = cur.dict[c - 'a'];
        }
        return true;
    }
    
    /** Delete word if it exists */
    public boolean delete(String word) {
        if (!search(word)) return false;
        
        TrieNode cur = root;
        for (char c : word.toCharArray()) {
            TrieNode next = cur.dict[c - 'a'];
            if (next.count == 1) {
                cur.dict[c - 'a'] = null;
                return true;
            } else {
                next.count--;
                cur = next;
            }
        }
        
        cur.word = null;
        return true;
    }
    
    /** Return all the words in trie */
    public List<String> allWords() {
        List<String> words = new ArrayList();
        allWords(root, words);
        return words;
    }
    
    public void allWords(TrieNode root, List<String> words) {
        if (root == null) return;
        if (root.word != null) words.add(root.word);
        for (TrieNode node : root.dict)
            allWords(node, words);
    }
    
    class TrieNode {
        TrieNode[] dict;
        int count = 0;
        String word = null; // boolean isEnd = false;
        
        TrieNode() {
            dict = new TrieNode[26];
        }
    }
}
```

