---
layout: post
title: Data structures - A new perspective
date: 2026-06-20
author: Harikrishna Mohan
categories:
  - Concepts
tags:
  - Arrays
  - Basics
---
When we learn about various data structures, it is easy to get lost in all the complexities and miss a surprisingly simple idea underneath all of them:

> *A computer only knows how to read from and write to memory.*

Everything running in a computer is built on top of that memory. So before delving into data structures era, let's start from that fundamental idea and build our intuition step by step.
## Memory is just an array
We can think of computer memory as a collection of cells, where each cell is arranged on a line of finite length and store some basic data within it. These cells are labeled using a sequential number called an address.
<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/line-of-cells.png" style="width: 100%; max-width: 320px; margin: 0 auto;">
</div>

As long as we know the address of a cell, the computer allows us to perform two basic operations.

1. reading data from an address
```python
data = memory[1];
```
2. Writing data to an address
```python
memory[3] = data;
```

This simple arrangement of memory naturally brings us to the concept of an array in programming. In array, we use an index to point to a location where data is to be read or written. In software terms, computer memory is a large array with indices presented as address. In the end, everything a computer has, runs on this array and, uses the only core functionalities it provides. That is, writing data to an index and reading data from an index.

Keeping that perspective in mind, let's understand why do we need data structures at all.

### The searching problem
Let us consider an array with many elements, and we need to find a specific element using the fundamental operations we have. Assuming, the array is not arranged in any order, we will end up searching the entire array until we find that element. This requires a lot of computing if the size of array is large.
<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/unsorted-array-example.png" style="width: 100%; max-width: 520px; margin: 0 auto;">
</div>
We can reduce this computation significantly by sorting the array in ascending order.

Now suppose we want to find the element 'Z' from the array. Since the array is sorted, just by looking at the last index in the array, we can conclude whether or not 'Z' is present in the array without ever looking anywhere else in the array.
<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/sorted-array-example.png" style="width: 100%; max-width: 520px; margin: 0 auto;">
</div>

By sorting the array, we didn't add any new hardware capabilities. The computer still performs the same basic operations we saw earlier. However, by identifying properties of the data stored in the array, we exploited it's ordering; in order to achieve incredibly fast searching speeds.

### The insertion problem
Let's explore this pattern in another scenario.
Suppose we frequently need to insert new elements at arbitarary positions of an array. Since arrays store its elements sequentially, inserting a single element may require shifting many existing elements one position to the right.
<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/inserting-at-middle-example.png" style="width: 100%; max-width: 320px; margin: 0 auto;">
</div>
If the array is huge and insertions happen often, this shifting process becomes expensive.

We can pack multiple data fields into one cell using a user-defined type.  
```c
struct node {
	int value;
	int next_node_index;
};
```
Now each node in the array not only stores its value, but also the index of the next node.
By following the *next_node_index* field from the starting node, we can reach any node that belongs to the chain of nodes.

<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/ll-using-array-example.png" style="width: 100%; max-width: 420px; margin: 0 auto;">
</div>

 Using this structure, allows us to place nodes anywhere in the array without worring about sequential ordering of arrays. To insert a new element in the middle, we no longer need to shift half the array. We insert the new node anywhere on the array and simply change a few indices so that the new element becomes part of the chain.
<div style="text-align: center; margin: 1rem 0;">
<img src="{{ site.baseurl }}/assets/ll-inserting-new-element-example.png" style="width: 100%; max-width: 520px; margin: 0 auto;">
</div>
Now inserting an element in the middle is extremely fast. Again, we didn't add any new hardware capabilities. The computer still performs the exact same read and write operations on memory. We only organized the data differently and exploited a new property of that organization.

## So what is a data structure?
Let's distill the patterns we observed so far.
At the lowest level, everything in a computer lives in memory. Since memory is just a large array, every operation eventually reduces to reading from or writing to a particular array index. For figuring out that index, different ways of organizing data create different relationships between indices, and each organization comes with its own strengths and weaknesses that we can exploit.

> A data structure is simply a way of organizing data in memory so that the indices we need can be found efficiently.

Arrays optimize random access.

Linked lists optimize insertion and deletion.

Trees optimize hierarchical searching.

Hash tables optimize lookup using keys.

But underneath all of them, the computer is still doing the exact same thing. Everything else is just clever organization.

---
