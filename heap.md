# Heap

```java
class Heap<T extends Comparable<T>> {
    private T[] arr;
    private int size, capacity;
    
    Heap(int capacity) {
        this.capacity = capacity;
        size = 0;
        arr = (T[])new Comparable[capacity];
    }
    
    private int left (int i) {
        return i << 1;
    }
    
    private int right (int i) {
        return (i << 1) + 1;
    }
    
    private int parent (int i) {
        return i / 2;
    }
    
    public void offer(T t) {
        if (size == capacity - 1) return;
        arr[++size] = t;
        shiftUp(size);
    }
    
    private void shiftUp(int i) {
        int p = parent(i);

        while (p > 0 && arr[i].compareTo(arr[p]) < 0) {
            swap(i, p);
            i = p;
            p = parent(p);
        }
    }
    
    public T pop() {
        if (size == 0) return null;
        
        T r = arr[1];
        swap(1, size--);
        shiftDownIterative(1);
        return r;
    }
    
    private void shiftDownRecursive (int i) {
        int l = left(i), r = right(i), m = i;

        if (l <= size && arr[l].compareTo(arr[m]) < 0) m = l;
        if (r <= size && arr[r].compareTo(arr[m]) < 0) m = r;

        if (m != i) {
            swap(i, m);
            shiftDownRecursive(i);
        }
    }
    
    private void shiftDownIterative (int i) {
        int l = left(i), r = right(i), m = i;

        while (l <= size) {
            if (l <= size && arr[l].compareTo(arr[m]) < 0) m = l;
            if (r <= size && arr[r].compareTo(arr[m]) < 0) m = r;

            if (m == i) break;
            
            swap(i, m);
            i = m;
            l = left(i);
            r = right(i);
        }
    }
    
    private void swap(int i, int j) {
        T t = arr[i];
        arr[i] = arr[j];
        arr[j] = t;
    }
    
    public int size() {
        return size;
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public void print() {
        for (int i = 1; i <= size; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }
}
```

