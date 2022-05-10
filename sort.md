## Sort
## Bubble Sort
```java
// O(n^2)
public static int[] bubbleSort(int[] arr){
    if(arr.length == 0) return arr;
    for(int i = 0; i < arr.length; i++){
        for(int j = 0; j < arr.length - 1 - i; j ++){
            if(arr[j + 1] < arr[j]){
                int tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
    return arr;
}
```

## Selection Sort
```java
// O(n^2)
public static int[] selectionSort(int[] arr){
    if(arr.length == 0) return arr;
    for(int i = 0; i < arr.length; i++){
        int minIndex = i;
        for(int j = i; j < arr.length; j++){
            if(arr[j] < arr[minIndex]) minIndex = j;
        }
        int temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
    return arr;
}
```

## Insertion Sort
```java
// O(n^2)
public static int[] insertionSort(int[] arr){
    if(arr.length == 0) return arr;
    int current;
    for(int i = 0; i < arr.length - 1; i++){
        current = arr[i + 1];
        int preIndex = i;
        while(preIndex >= 0 && current < arr[preIndex]){
            arr[preIndex + 1] = arr[preIndex];
            preIndex --;
        }
        arr[preIndex + 1] = current;
    }
    return arr;
}
```

## Merge Sort
```java
//O(nlogn)
public static int[] mergeSort(int[] arr){
    if(array.length < 2) return arr;
    int mid = arr.length / 2;
    int[] left = Arrays.copyOfRange(arr, 0, mid);
    int[] right = Arrays.copyOfRange(arr, mid, arr.length);
    return merge(mergeSort(left), mergeSort(right));
}

public static int[] merge(int[] left, int[] right){
    int[] result = new int[left.length + right.length];
    for(int index = 0, i = 0, j = 0; index < result.length; index++){
        if(i >= left.length) result[index] = right[j++];
        else if(j >= right.length) result[index] = left[i++];
        else if(left[i] > right[j]) result[index] = right[j++];
        else result[index] = left[i++];
    }
    return result;
}
```

## Quick Sort
```java
//O(nlogn)
public static int[] quickSort(int[] arr, int start, int end){
    if(arr.length < 1 || start < 0 || end >= arr.length || start > end) return null;
    int smallIndex = partition(arr, start, end);
    if(smallIndex > start) quickSort(arr, start, smallIndex - 1);
    if(smallIndex < end) quickSort(arr, smallIndex + 1, end);
    return arr;
}

public static int partition(int[] arr, int start, int end){
    int pivot = (int) (start + Math.random() * (end - start + 1));
    int smallIndex = start -1;
    swap(arr, pivot, end);
    for(int i = start; i <= end; i++){
        if(arr[i] <= arr[end]){
            smallIndex++;
            if(i > smallIndex) swap(arr, i, smallIndex);
        }
    }
    return smallIndex
}

public static void swap(int[] arr, int i, int j){
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```