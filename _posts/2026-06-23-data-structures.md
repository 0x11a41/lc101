---
layout: post
title: Data structures
date: 2026-06-23
categories: [ Concepts ]
tags: [ Arrays, Basics ]
author: hari
author_url: https://github.com/0x11a41
---
When we learn about data structures, it is easy to get our minds lost in all the complexities and miss a surprisingly simple idea underneath all of them:

> *A computer only knows how to read from and write to memory.*

Everything running on a computer is built on top of that memory. So before delving into data structures era, let's start from that fundamental idea and build our intuition step by step.
## Memory is just an array
We can think of computer memory as a collection of cells, where each cell is arranged on a line of finite length and store some basic data within it. These cells are labeled using a sequential number called an address.
<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/line-of-cells.png" style="max: clamp(0, 100%, 320px);">
</div>

As long as we know the address of a cell, the computer allows us to perform two basic operations.

1. reading data from an address
```c
char data = memory[1];
```
2. Writing data to an address
```c
memory[3] = data;
```

This simple arrangement of memory naturally brings us to the concept of an array in programming. In array, we use an index to point to a location where data is to be read or written. In software terms, computer memory is a large array with indices presented as address. In the end, everything a computer has, runs on this array and, uses the only core functionalities it provides. That is, reading data from an index and writing data to an index.

Keeping that perspective in mind, let's understand why do we need data structures at all.

### The searching problem
Let us consider an array with many elements, and we need to find a specific element using the fundamental operations we have. Assuming, the elements are not arranged in any order, we mostly will end up searching the entire array until we find that element. This requires a lot of computing if the size of array is large.
<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/unsorted-array-example.png" style="max: clamp(0, 100%, 520px);">
</div>
We can reduce this computation significantly by sorting the array in ascending order.

Now suppose we want to find the element 'Z' from the array. Since the array is sorted, just by looking at the last index in the array, we can conclude whether or not 'Z' is present in the array without ever looking anywhere else in the array.
<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/sorted-array-example.png" style="max: clamp(0, 100%, 520px);">
</div>

By sorting the array, we didn't add any new hardware capabilities. The computer still performs the same basic operations we saw earlier. However, by identifying properties of the data stored in the array, we exploited it's ordering; in order to achieve incredibly fast searching speeds.

### The insertion problem
Let's explore this pattern in another scenario.
Suppose we frequently need to insert new elements at arbitary positions of an array. Since arrays store its elements sequentially, inserting a single element may require shifting many existing elements one position to the right.
<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/inserting-at-middle-example.png" style="max: clamp(0, 100%, 320px);">
</div>
If the array is huge and insertions happen often, this shifting process becomes expensive.

We can pack multiple data fields into one cell using a user-defined type.  
```c
struct cell {
	int data;
	int next_cell_index;
};
```
Now each cell in the array not only stores data, but also the index of the next cell.
By following the *next_cell_index* field from the starting index, we can reach any element that belongs to the chain of cells.

<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/ll-using-array-example.png" style="max: clamp(0, 100%, 420px);">
</div>

 Using this structure, allows us to place elements anywhere in the array without worring about sequential ordering of arrays. To insert a new element in the middle, we no longer need to shift half the array. We insert the new cell anywhere on the array and simply change a few indices so that the new element becomes part of the chain.
<div class="diagrams-wrapper">
	<img src="{{ site.baseurl }}/assets/data-structures/ll-inserting-new-element-example.png" style="max: clamp(0, 100%, 520px);">
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
