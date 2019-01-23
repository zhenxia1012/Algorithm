# Segment Tree

[Introduction][https://blog.csdn.net/coolkid_cwm/article/details/52137427]
<b>

### Normal Version

e.g. minimum value in [i, j]

```java
public Node buildTree(int[] nums, int start, int end) {
    if (start > end) return null;
    
    Node root = new Node(start, end);
    if (start == end) {
        root.min = nums[start];
        return root;
    }
    
    int mid = (start + end) / 2;
    root.left = buildTree(nums, start, mid);
    root.right = buildTree(nums, mid + 1, end);
    root.min = Math.min(root.left.min, root.right.min);
    
    return root;
}

public int query(Node root, int start, int end) {
    if (start > root.rv || end < root.lv) return Integer.MAX_VALUE;
    if (start <= root.lv && end >= root.rv) return root.min;
    return Math.min(query(root.left, start, end), query(root.right, start, end));
}

public void update(Node root, int start, int end, int val) {
    if (start > root.rv || end < root.lv) return;
    if (root.lv == root.rv) root.min += val;
    else {
        update(root.left, start, end, val);
        update(root.right, start, end, val);
        root.min = Math.min(root.left.min, root.right.min);
    }
}

// if have update, don't need this function
public void change(Node root, int p, int val) {
    if (p > root.rv || p < root.lv) return;
    if (root.lv == p && p == root.rv) root.min = val;
    else {
        change(root.left, p, val);
        change(root.right, p, val);
        root.min = Math.min(root.left.min, root.right.min);
    }
}

class Node {
    int lv, rv;
    Node left, right;
    int min = Integer.MAX_VALUE;
    
    Node(int lv, int rv) {
        this.lv = lv;
        this.rv = rv;
        left = right = null;
    }
}
```
<b>

### Optimization1 - Lazy Tag

e.g. minimum value in [i, j]

```java
public Node buildTree(int[] nums, int start, int end) {
    if (start > end) return null;
    
    Node root = new Node(start, end);
    if (start == end) {
        root.min = nums[start];
        return root;
    }
    
    int mid = (start + end) / 2;
    root.left = buildTree(nums, start, mid);
    root.right = buildTree(nums, mid + 1, end);
    root.min = Math.min(root.left.min, root.right.min);
    
    return root;
}

public int query(Node root, int start, int end) {
    if (start > root.rv || end < root.lv) return Integer.MAX_VALUE;
    if (start <= root.lv && end >= root.rv) return root.min;
    pushDown(root);
    return Math.min(query(root.left, start, end), query(root.right, start, end));
}

public void update(Node root, int start, int end, int val) {
    if (start > root.rv || end < root.lv) return;
    if (start <= root.lv && end >= root.rv) {
        root.min += val;
        root.delta += val;
    } else {
        pushDown(root);
        update(root.left, start, end, val);
        update(root.right, start, end, val);
        root.min = Math.min(root.left.min, root.right.min);
    }
}

// if have update, don't need this function
public void change(Node root, int p, int val) {
    if (p > root.rv || p < root.lv) return;
    if (root.lv == p && p == root.rv) root.min = val;
    else {
        pushDown(root);
        change(root.left, p, val);
        change(root.right, p, val);
        root.min = Math.min(root.left.min, root.right.min);
    }
}

public void pushDown(Node root) {
    if (root.delta == 0) return;
    root.left.min += root.delta;
    root.left.delta += root.delta;
    root.right.min += root.delta;
    root.right.delta += root.delta;
}

class Node {
    int lv, rv;
    Node left, right;
    int min = Integer.MAX_VALUE;
    int delta = 0;
    
    Node(int lv, int rv) {
        this.lv = lv;
        this.rv = rv;
        left = right = null;
    }
}
```
<b>

### Optimization2 - Lazy Initilization

e.g. count of values in [i, j]

```java
public Node buildTree(int start, int end) {
    return new Node(start, end);
}

public int query(Node root, int val) {
    if (val >= root.rv) return root.cnt;
    if (val < root.lv) return 0;
    return query(root.getLeft(), val) + query(root.getRight(), val);
}

public void insert(Node root, int val) {
    if (val < root.lv || val > root.rv) return;
    if (root.lv == p && p == root.rv) root.cnt++;
    else {
        insert(root.getRight(), val);
        insert(root.getLeft(), val);
        root.cnt = root.getLeft().cnt + root.getRight().cnt;
    }
}

class Node {
    int lv, rv;
    Node left, right;
    int cnt = 0;
    
    Node (int lv, int rv) {
        this.lv = lv;
        this.rv = rv;
    }
    
    public int getMid() {
        return lv + (rv - lv) / 2;
    }
    
    public Node getLeft() {
        if (left == null) left = new Node(lv, getMid());
        return left;
    }
    
    public Node getRight() {
        if (right == null) right = new Node(getMid() + 1, rv);
        return right;
    }
}
```
