---
layout: post
title:  "ALG-Week1 Basic Sort Algorithm"
date:   2018-06-19 12:35:18 +1000
categories: algorithm
---

Selection Sort, Insertion sort and Shellsort are three basic sort algorithm. Some of them are more efficient than the other complicated algorithms in some specific situations.

First, create a function to swap two elements in a vector:

```c++
void swap(vector<int> &v, int i1, int i2) {
    int temp = v[i1];
    v[i1] = v[i2];
    v[i2] = temp;
}
```

# Selection Sort 选择排序
Selection sort keep choosing the smallest number in the rest. For example, if the first element is the smallest one, this algorithm will swap the element with itself.

Suppose an array with length `N`, in selection sort, the total swapping time is `N`.
In the worst circumstance, the comparing time is `N ^ 2 / 2`.

For every element in the array, this algorithm will go through the rest array to look for the smallest one, although the first one is the smallest. It means even an sorted array, selection sort will cost the same time as a random one.

用选择排序进行从小到大排列，即选出未排序队列中最小的元素，加入有序队列的末尾。
对于一个长度为 `j` 的队列，假设前 `i` 项已经排序完成。则选取剩余 `j - i` 项中最小的元素，与 `i + 1` 项元素调换位置。

```c++
void selection_sort(vector<int> &v) {
    for (int i = 0; i < v.size(); i++) {
        int smallest = v[i];
        int s_index = i;
        for (int j = i; j < v.size(); j++) {
            if (v[j] < smallest) {
                smallest = v[j];
                s_index = j;
            }
        }
        swap(v, i, s_index);
    }
}
```

# Insertion sort 插入排序
Insertion sort means choosing the next element and insert it to the right position.
A sorted array just do `N` times comparasion and it's more efficient than the other sort algorithm.

用插入排序进行从小到大排列，即将单个元素插入到已排序完毕的队列中。
假设队列中前 `i - 1` 个元素已经按顺序排列，对于第 `i` 个元素，如果它小于第 `i - 1` 个元素，则将二者调换位置，并继续对 `i - 1` 和 `i - 2` 元素进行对比，直至建立一个 `i` 个元素的有序队列。
```c++
void insertion_sort(vector<int> &v) {
    for (int i = 1; i < v.size(); i++) {
        int j = i;
        while (v[j] < v[j - 1]) {
            swap(v, j, j - 1);
            j--;
            if (j == 0) break;
        }
    }
}
```

# Shellsort 希尔排序
插入排序的一个缺点是，如果将一个元素的初始位置偏离太远，则需要多次交换才能将元素插入其正确的位置。在元素容量较大的数组中，这种操作将会非常耗时。

用希尔排序进行从小到大排列，以下面代码为例，先按 1, 4, 13, 40... 的序列生成数字，然后将要排序的列表依次按每 40 个一组，每 13 个一组，每 4 个一组的顺序进行插入排序。希尔排序是一种有效的处理插入排序缺点的一种改进。

希尔排序代码量小，而且不需要占用额外的内存空间，对于中等大小的数组它的运行时间是可以接受的。虽然某些算法(快速排序等)更加高效，但是他们也只能带来常数倍的速度提升，并且更为复杂。如果需要排序算法时，先使用希尔排序，然后再根据运行情况考虑是否值得将其替换为更为复杂的排序方式。
```c++
void shellsort(vector<int> &v) {
    int init = 1;
    while (init < v.size()) init = init * 3 + 1;

    while (init /= 3 > 0) {
        for (int i = init; i < v.size(); i += init) {
            int j = i;
            while (v[j] < v[j - init]) {
                swap(v, j, j - init);
                j -= init;
                if (j == 0) break;
            }
        }
    }
}
```