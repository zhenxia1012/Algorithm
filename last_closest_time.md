# Last Closest Time



## Description

要求返回最近的时间，可以重复使用数字，比如'19:35' 返回'19:33'.

hint: [681 - next closest time][[https://www.baidu.com/]
<b>


## Solution

#### Iterative

```java
public String nextClosestTime(String time) {
	 Set<Integer> set = new HashSet<Integer>();
     for (char c : time.toCharArray()) {
        if (c != ':') set.add(c - '0');
     }
     

    int cur = Integer.parseInt(time.substring(0, 2)) * 60 
            + Integer.parseInt(time.substring(3));
    int next = cur, dif = 1440;
    for (int i1 : set) for (int i2 : set) {
        if (i1 * 10 + i2 >= 24) continue;
        for (int i3 : set) for (int i4 : set) {
            if (i3 * 10 + i4 >= 60) continue;
            int tem = i1 * 600 + i2 * 60 + i3 *10 + i4;
            int d = cur - tem > 0 ? cur - tem : (1440 + cur - tem);
            if (d < dif) {
                next = tem;
                dif = d;
            }
        }
    }
    
    return String.format("%02d:%02d", next / 60, next % 60);
}
```

__Time__: O(256);  __Space__: O(4)

***

#### Greedy

``` java
public String nextClosestTime(String time) {
     char[] t = time.toCharArray();
     TreeSet<Character> set = new TreeSet<Character>();
     for (char c : t) {
         if (c != ':') set.add(c);
     }
     

    char[] ch = new char[set.size()];
    for (int i = 0; i < ch.length; ++i)
        ch[i] = set.pollFirst();
    
    for (int i = t.length - 1; i >= 0; --i) {
        if (t[i] == ':') continue;
        
        int p = Arrays.binarySearch(ch, t[i]);
        if (p == 0) t[i] = ch[ch.length - 1];
        else {
            char n = ch[p - 1];
            t[i] = n;
            break;
        }
    }
    
    return new String(t);
}
```

**Time**: O(4);  **Space**: O(4)
