---
layout: post
title:  "ALG-Week0 Basic Data Structure"
date:   2018-06-15 22:43:30 +1000
categories: algorithm
---

## 1 Array
### 1.1 创建数组
```java
double[] a = new double[5];
double[] a = {1, 2, 3, 4, 5};
```

### 1.2 典型数组处理
```java
double[] array = {4, 2, 1, 6, 3, 5};

// find the biggest element
double max = array[0];
for (int i = 0; i < array.length; i++) {
    if (array[i] > max)
        max = array[i];
}

// find the average of the array
double sum = 0.0;
for (int i = 0; i < array.length; i++)
    sum += array[i];
double avg = sum / array.length;

// duplicate an array
double[] new_array = new double[array.length];
for (int i = 0; i < array.length; i++)
    new_array[i] = array[i];

// reverse an array
double[] rev_array = new double[array.length];
for (int i = 0 ; i < array.length; i++)
    new_array[i] = array[array.length - 1 - i];
```

### 1.3 二分查找
```java
public static int rank(int val, int[] array) {
    int lo = 0; int hi = array.length;
    while (lo <= hi) {
        int mi = (lo + hi) / 2;
        if (val < array[mi])
            hi = mi - 1;
        else if (val > array[mi])
            lo = mi + 1;
        else
            return mi;
    }
    return -1;
}
```

## 2 Bag, Queue and Stack
### 2.1 API
```java
public class Bag<Item> implements Iterable<Item> {
    public Bag() // constructor
    public void add(Item item) // add an element
    public boolean isEmpty() // return if the bag is empty
    public int size() // return the number of elements
}

public class Queue<Item> implements Iterable<Item> {
    public Queue() // constructor
    public void enqueue(Item item) // add an element
    public Item dequeue() // remove the first element
    public boolean isEmpty() // return if the queue is empty
    public int size() // return the number of the element
}

public class Stack<Item> implements Iterable<item> {
    public Stack() // constructor
    public void push(Item item) // add an element
    public Item pop() // remove the last element
    public boolean isEmpty() // return if the stack is empty
    public int size() // return the number of the element
}
```

### 2.2 Dijkstra's Two-stack Algorithm
```java
public static Double dtsa(String exp) {
    Stack<String> ops = new Stack<String>();
    Stack<Double> vals = new Stack<Double>();
    for (int i = 0; i < exp.length(); i++) {
        String this_char = exp.charAt(i) + "";
        if (this_char.equals("("));
        else if (this_char.equals("+") || this_char.equals("-")
                || this_char.equals("*") || this_char.equals("/"))
                ops.push(this_char);
        else if (this_char.equals(")")) {
            String op = ops.pop();
            Double v = vals.pop();
            if (op.equals("+")) v += vals.pop();
            else if (op.equals("-")) v -= vals.pop();
            else if (op.equals("*")) v *= vals.pop();
            else if (op.equals("/")) v = vals.pop() / v;
            vals.push(v);
        } else {
            vals.push(Double.parseDouble(this_char));
        }
    }
    return vals.pop();
}
```

### 2.3 Implement Bag, Queue, Stack with Linked List
First, we should have a node of linked list. A node holds an item and point to the next node.
```java
private class Node {
    Item item;
    Node next;
}
```

```java
// implement bag with linked list
public class Bag<Item> implements Iterable<Item> {
    private Node first;
    private int num;
    private class Node {
        Item item;
        Node next;
    }

    public boolean isEmpty() { return first == null; }
    public int size() { return num; }
    public void add(Item item) {
        Node previous = first;
        first = new Node();
        first.item = item;
        first.next = previous;
        num++;
    }
}
```

```java
// Implement stack with linked list
public class Stack<Item> implements Iterable<Item> {
    private Node first;
    private int num;
    private class Node {
        Item item;
        Node next;
    }

    public boolean isEmpty() { return first == null; }
    public int size() { return num; }
    public void push(Item item) {
        Node previous = first;
        first = new Node()
        first.item = item;
        first.next = previous;
        num++;
    }
    public Item pop() {
        Item item = first.item;
        first = first.next;
        num--;
        return item;
    }
}
```

```java
// Implement queue with linked list
public class Queue<Item> implements Iterable<Item> {
    private Node first;
    private Node last;
    private int num;
    private class Node {
        Item item;
        Node next;
    }

    public boolean isEmpty() { return first == null; }
    public int size() { return num; }
    public void enqueue(Item item) {
        Node previous = last;
        last = new Node();
        last.item = item;
        last.next = null;
        if (isEmpty())
            first = last;
        else
            previous.next = last;
        num++;
    }
    public Item dequeue() {
        Item item = first.item;
        first = first.next;
        if (isEmpty())
            last = null;
        num--;
        return item;
    }
}
```

