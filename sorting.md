# Sorting



###Bubble Sort

```java
public void bubbleSort(int[] nums) {
    for (int i = nums.length - 1; i > 0; i--) {
        for (int j = 0; j < i; j++) {
            if (nums[j] > nums[j + 1])
                swap(nums, j, j + 1);
        }
    }
}
```



### Selection Sort

```java
public void selectSort(int[] nums) {
	for (int i = 0; i < nums.length - 1; i++) {
		int k = i;
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] < nums[k])
                k = j;
        }
        swap(nums, i, k);
	}
}
```



### Insertion Sort

```java
public void insertSort(int[] nums) {
	for (int i = 1; i < nums.length; i++) {
		int j = i - 1;
		for (; j >= 0 && nums[j] > nums[i]; j--) {
			swap(nums, j, j +1 );
		}
		nums[j + 1] = nums[i];
	}
}
```



### Quick Sort

```java
public void quickSort(int[] nums) {
		if (nums.length == 0) return;
		quickSort(nums, 0, nums.length - 1);
	}

	public void quickSort(int[] nums, int start, int end) {
		if (start >= end) return;
		int idx = partition(nums, start, end);
		quickSort(nums, start, idx - 1);
		quickSort(nums, idx + 1, end);
	}

	public int partition(int[] nums, int start, int end) {
		int p = nums[start], l = start + 1, r = end;
		
		while (l <= r) {
			while (l <= r && nums[l] <= p) l++;
			while (l <= r && nums[r] >= p) r--;
			if (l < r) swap(nums, l, r);
		}
		swap(nums, start, r);
		
		return r;
	}
}
```

