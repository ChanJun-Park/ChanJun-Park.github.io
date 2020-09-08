---
title: "[알고리즘] 퀵정렬(Quick Sort) 참고 코드"
date: 2020-09-08T15:34:30-04:00
classes: wide
categories:
  - Algorithm Theory
tags:
  - 퀵정렬
  - Quick Sort
---

```java
private static void quickSort(int[] arr, int first, int last) {
    if (first > last) return;
    
    int i = first;
    int j = last;
    int mid = first + (last - first) / 2;
    swap(arr, first, mid);

    int pivot = first;
    
    while(i < j) {
        while(i <= last && arr[i] <= arr[pivot]) i++;
        while(j >= first && arr[j] > arr[pivot]) j--;
        if (i < j) {
            swap(arr, i, j);
        }
    }
    swap(arr, pivot, j);

    quickSort(arr, first, j - 1);
    quickSort(arr, j + 1, last);
}

private static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```
