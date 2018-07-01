---
layout: post
title:  "ALG-Week1 merge-sort"
date:   2018-06-20 10:11:21 +1000
categories: algorithm
---

# 自顶向下的归并排序
自顶向下的归并排序是分治算法(divide-and-conquer)的一个最典型的例子。
如果要将一个长度为 `N` 的数组排列，先将这个数组分为两个长度为 `2/N` 的数组，分别对其排序，再将两者归并到一起。

```c++
void merge_sort(vector<int> &v, int lo, int hi) {
    if (hi <= lo) return;
    int mid = (lo + hi) / 2;
    merge_sort(v, lo, mid);
    merge_sort(v, mid + 1, hi);
    merge(v, lo, mid, hi);
}

void merge(vector<int> &v, int lo, int mid, int hi) {
    vector<int> temp = v;
    int left = lo;
    int right = mid + 1;

    for (int i = lo; i <= hi; i++) {
        if (left > mid) v[i] = temp[right++];
        else if (right > hi) v[i] = temp[left++];
        else if (temp[left] < temp[right]) v[i] = temp[left++];
        else v[i] = temp[right++];
    }
}
```

# 自底向上的归并排序
将一个数组两两元素归并为一组，再将两组归并为一组，直至整个数组排序完成。

```c++
void merge_sort(vector<int> &v, int lo, int hi) {
    for (int len = 1; len <= hi - lo; len *= 2) {
        for (int i = lo; i < hi; i += 1) {
            merge(v, lo, lo + len - 1, Math.min(lo + 2 * len - 1, hi))
        }
    }
}

void merge(vector<int> &v, int lo, int mid, int hi) {
    vector<int> temp = v;
    int left = lo;
    int right = mid + 1;

    for (int i = lo; i <= hi; i++) {
        if (left > mid) v[i] = temp[right++];
        else if (right > hi) v[i] = temp[left++];
        else if (temp[left] > temp[right]) v[i] = temp[right++];
        else v[i] = temp[left++];
    }
}
```

# 归并排序的性能
命题 1I: 没有任何基于比较的算法能够保证使用少于 `lg(N!)` ~ `NlgN` 次比较将长度为 `N` 的数组排序。
即是说，对于任意基于比较的排序算法来说，最坏情况下的比较次数，大于等于 `lg(N!)`。

证明: 因为对于长度为 `N` 的数组而言，共有 `N!` 种排列方式。基于比较的算法将数组内的元素进行两两比较，进行 `m` 次比较后，最多有 `2 ** m` 中排列组合方式。最理想情况下，`N!` 中排列方式能在 `lg(N!)` 次比较中产生。