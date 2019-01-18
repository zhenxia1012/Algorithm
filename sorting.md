# Sorting



### Bubble Sort

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



### Merge Sort

```java
private static void mergeSort(int[] a) {
    Sort(a, 0, a.length - 1);
}

private static void Sort(int[] a, int left, int right) {
    if(left>=right) return;

    int mid = (left + right) / 2;
    Sort(a, left, mid);
    Sort(a, mid + 1, right);
    merge(a, left, mid, right);

}


private static void merge(int[] a, int left, int mid, int right) {
    int[] tmp = new int[a.length];
    int r1 = mid + 1;
    int tIndex = left;
    int cIndex=left;

    while(left <=mid && r1 <= right) {
        if (a[left] <= a[r1]) 
            tmp[tIndex++] = a[left++];
        else
            tmp[tIndex++] = a[r1++];
    }

    while (left <= mid) tmp[tIndex++] = a[left++];
    while (r1 <= right) tmp[tIndex++] = a[r1++];

    while(cIndex<=right){
        a[cIndex]=tmp[cIndex];
        cIndex++;
    }
}
```



### Heap Sort

```java
void heapSort(int[] arr) {
    int len = arr.length;
    buildMaxHeap(arr, len-1);
    
    for(int i = len-1; i > 0; i--) {
        swap(arr, i, 0);
        maxHeapify(arr, 0, i-1);
    }
}

/** @bottom up */
void buildMaxHeap(int[] arr, int heapsize) {
    for(int i = (heapsize-1) / 2; i >= 0; i--)
        maxHeapify(arr,i,heapsize);
}

/** @top down */
// public void buildHeap(int[] nums) {
//     for(int i = 0; i < nums.length; i++){
//         int child = i;
//         int parent = (child - 1) / 2;
//         while(parent >= 0 && nums[parent] < nums[child]){
//             swap(nums, parent, child);
//             child = parent;           
//             parent = (child - 1) / 2;
//         }
//     }
// }

/** @recursion */
void maxHeapify(int[] arr, int i, int heapsize) {
    int left = 2 * i + 1, right = 2 * i + 2;
    int largest = i;
    
    if (left <= heapsize && arr[left] > arr[i])
        largest=left;
    if (right <= heapsize && arr[right] > arr[largest])
        largest=right;
    
    if(largest != i) {
        swap(arr, i, largest);
        maxHeapify(arr, largest, heapsize);
    }
}

/** @iterative */
// void maxHeapify(int[] arr, int i, int heapsize) {
//     int left = 2 * i + 1, right = 2 * i + 2;
//     int largest = i;
    
//     while (i < heapsize) {
//       if (left <= heapsize && arr[left] > arr[i])
// 	        largest=left;
// 	    if (right <= heapsize && arr[right] > arr[largest])
// 	        largest=right;
	    
// 	    if(largest != i) {
// 	        swap(arr, i, largest);
// 	        i = largest;
// 	        left = 2 * i + 1;
// 	        right = 2 * i + 2;
// 	    } else break;
//     }
// }
```

