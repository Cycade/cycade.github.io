---
layout: post
title:  "ALG-Week1 quicksort"
date:   2018-06-22 11:58:09 +1000
categories: algorithm
---

# 快速排序
快速排序首先确定一个`切分元素`，通常情况下为数组的第一个元素，然后根据与`切分元素`的比较，将原数组分为两部分，小于等于`切分元素`的部分和大于等于`切分元素`的部分，最后将小于等于的部分的最后一个元素与`切分元素`交换位置。之后进入对两部分的快速排序，直至排序完成。

```c++
void quicksort(vector<int> &v, int lo, int hi) {
    if (lo >= hi) return;
    int pt = partition(v, lo, hi);
    quicksort(v, lo, pt - 1);
    quicksort(v, pt + 1, hi);
    std::cout << pt << std::endl;
}

int partition(vector<int> &v, int lo, int hi) {
    int i = lo + 1; int j = hi;
    while (i <= j) {
        while(v[i] <= v[lo] && i <= hi) i++;
        while(v[j] >= v[lo] && j >= lo + 1) j--;
        if (i <= j) swap(v, i, j);
    }
    swap(v, lo, j);
    return j;
}

void swap(vector<int> &v, int i1, int i2) {
    int temp = v[i1];
    v[i1] = v[i2];
    v[i2] = temp;
}
```