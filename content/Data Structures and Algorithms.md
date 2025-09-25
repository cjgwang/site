---
title: Data Structures and Algorithms in Python
draft: false
tags:
---
Contents:
1. Arrays
2. Linked Lists
3. Hash Tables
4. Stacks
5. Queues
6. Heaps / Priority Queues
7. Sorting
	1. Bubble Sort
	2. Quick Sort
8. Recursion
9. Binary Search
10. Two Pointers
11. Tries

### Arrays
Arrays are a dynamic array. Python does not have static arrays.

Q: What is the value of the 1st number?
indexing: list[0], list[1]
This is O(1), constant time. 

Q: What position is x value?
```
for i in range(len(list)):
	if list[i]== x:
		return i
```
O(n)

Q: print all values:
```
for i in list:
	print(i)
```
O(n)

Q: insert new value
list.insert(index, value)
O(n) -> shifts other numbers up

Q: delete a value
list.remove(index)
O(n) -> shifts other numbers down

Check for duplicates
```
def hasDuplicate(self, nums: List[int]) -> bool:
    # Brute force
    for i in range(len(nums)):
        for j in range(i+1, len(nums)):
            if nums[i] == nums[j]:
                return True
    return False
```

### Linked Lists
Issues with array: inefficient use of memory for pre-allocated spaces, esp during insertion
Linked lists solve this by allowing you to access different elements, since you don't need to pre-allocate space and insertion at the start is easier

```
class Node:
    def __init__(self, data=None, next=None):
        self.data = data # any data in node
        self.next = next # pointer to next element
    
class LinkedList:
    def __init__(self):
        self.head = None # points to head of linked list
    
    def insert_at_beginning(self, data):
        node = Node(data, self.head) # next value is current head
        self.head = node
    
    def print(self):
        if self.head is None:
            print("Linked list is empty.")
            return
        else:
            itr = self.head # iterator
            llstr = "" # linked list string 
            while itr:
                llstr += str(itr.data) + "->"
                itr = itr.next
        
        print(llstr)
    
    def insert_at_end(self, data):
        if self.head is None: #linked list is blank
            self.head = Node(data, None)
            return
        itr = self.head
        while itr.next:
            itr = itr.next
        
        itr.next = Node(data, None)

    def insert_values(self, data_list):
        self.head = None
        for data in data_list:
            self.insert_at_end(data)

    def get_length(self):
        length = 0
        itr = self.head
        while itr:
            length += 1
            itr = itr.next
        return length

    def remove_at(self, index):
        if index<0 or index>=self.get_length():
            raise Exception
        if index == 0: 
            self.head = self.head.next()
            return

        count = 0
        itr = self.head
        while itr:
            if count == index-1:
                itr.next = itr.next.next
                break
            itr = itr.next
            count += 1

    def insert_at(self, index, data):
        if index<0 or index>self.get_length():
            raise Exception
        if index == 0:
            self.insert_at_beginning(data)
            return
        
        count = 0
        itr = self.head
        while itr:
            if count == index-1:
                node = Node(data, itr.next)
                itr.next = node
                break
            itr = itr.next
            count += 1

if __name__ == "__main__":
    ll = LinkedList()
    ll.insert_values([1, 2])
    ll.remove_at(1)
    ll.insert_at(1, 3)
    ll.print()


```

Q:
```
def insert_after_value(self, data_after, data_insert):
	#search for first occurance of data_after
	#insert data_insert after data_after

def remove_by_value(self, data):
	#remove first node with data
```

### Hash Tables
Initialising a dict
```
dict = {}
with open("dict.csv", r) as f:
	for line in f:
		tokens = line.split(",")
		column_1 = tokens[0]
		column_2 = tokens[1]
		dict[column_1] = column_2
		

```
Dicts are O(1) compared to 2d lists are O(n). Insertion and deletion in dict is also O(1. )
Hash function converts key to value. 

Implementing a hash table
```
class HashTable:
    def __init__(self):
        self.MAX = 100
        self.arr = [None for i in range(self.MAX)]
    
    def get_hash(self, key):
        h = 0
        for char in key:
            h += ord(char)
        return h % 100
    
    def __setitem__(self, key ,value):
        h = self.get_hash(key)
        self.arr[h] = value

    def __getitem__(self, key):
        h = self.get_hash(key)
        return self.arr[h]
    
if __name__ == "__main__":
    t = HashTable()
    t["march"] = 3
    print(t["march"])
```

### Stacks
Last in first out (LIFO)
For linked list, you would have to traverse to the end, and with the array, you would need to use a dynamic array.
Push/pop: O(n)
Search element by value: O(n)

Implemented in python using list, collections.deque, queue.Lifoqueue

Using a list:
```
s = []

# to push:
s.append('jan')
s.append('feb')

# to get last element:
print(s[-1])

# to retrieve and remove last element:
s.pop()
```

The problem with arrays is memory issues with appending new elements, so using a list is not recommended. 

Using collections.deque:
Implemented using doubly-linked lists, so there is no issue with memory reallocation and copying data. 
```
from collections import deque

stack = deque()

# to push:
stack.append("jan")
stack.append("feb")
stack.append("mar")

# to retrieve remove last element
stack.pop()

```

Implementing a Stack class:
```
class Stack:
    def __init__(self):
        self.container = deque()
    
    def push(self, val):
        self.container.append(val)
    
    def peek(self):
        return self.container[-1]
    
    def is_empty(self):
        return len(self.container) == 0
    
    def pop(self):
        self.container.pop()
    
    def size(self):
        return len(self.container)
    
stack_1 = Stack()
stack_1.pop
```

### Queues
First in first out
Implemented in python using list, collections.deque, queue.LifoQueue

Implemented as a list:
```
#implemented as a list

q = []

#insert elements
q.insert(0, "jan")
q.insert(0, "feb")

# remove elements
q.pop()
```
Same issues as stacks - memory allocation and data copying

Implemented using collections.deque:
```
from collections import deque
queue = deque()

#insert elements
queue.appendleft("jan")
queue.appendleft("feb")
queue.appendleft("mar")

#remove elements
queue.pop()
```

Implemened as a Queue class
```
class Queue:
    def __init__(self):
        self.buffer = deque()
    
    def enqueue(self, val):
        self.buffer.appendleft(val)
    
    def dequeue(self):
        return self.buffer.pop()

    def is_empty(self):
        return len(self.buffer) == 0
    
    def size(self):
        return len(self.buffer)
```

### Heaps and Priority Queue
Uses heapq

A heap orders elements by priority and gives you the element with the higest priority/lowest priority number. 
Max heap and min heap
A heap makes it easier to insert data: O(log(n)), since you insert it at the end and you run heapify

Min heap:
```
import heapq

data = [23,5,12,6,123,73,1]

heap_data = heapq.heapify(data)

print(data)

# next element:
print(heapq.heappop(data))
# automatically heapifies data compared to data.pop()

#insert data:
heapq.heappush(data, 2) #automatically heapify
print(data)
```

You need to invert everything to make it into a max heap:
```
data = [-x for x in data]

#OR
heapq._heapify_max(data)
heapq._heappop_max(data)
```

Merging lists into a heap:
```
# merging lists into a heap
l1 = [1,2,3,4,5]
l2 = [5,4,3,2,1]

l3 = heapq.merge(l1, l2)
```

### Sorting
#### Bubble sort: O(n^2)
```
#O(n^2)

def bubble_sort(elements):
    size = len(elements)
    for j in range(size-1):
        swapped = False
        for i in range(size-1-j):
            if elements[i] > elements[i+1]:
                store = elements[i]
                elements[i] = elements[i+1]
                elements[i+1] = store
                swapped = True
        if not swapped:
            break
    return elements


if __name__ == "__main__":
    elements = [3, 1, 34, 67, 1, 4, 32, 87]
    print(bubble_sort(elements))
```

#### Quick sort:
O(nlog(n))
```
# Hoare's partition

def swap(a, b, arr):
    if a != b:
        arr[a], arr[b] = arr[b], arr[a]

def partition(elements, start, end):
    pivot_index = start
    pivot = elements[pivot_index]

    while start < end:
        while start < len(elements) and elements[start] <= pivot:
            start += 1
        
        while elements[end] > pivot:
            end -= 1
        
        if start < end:
            swap(start, end, elements)

    swap(pivot_index, end, elements)
    return(end)

def quick_sort(elements, start, end):
    if start < end:
        p1 = partition(elements, start, end)
        quick_sort(elements, start, p1-1)
        quick_sort(elements, p1 + 1, end)

if __name__ == "__main__":
    elements = [11, 9, 29, 7, 2, 15, 28]
    quick_sort(elements, 0, len(elements)-1)
    print(elements)
```

### Recursion
1. Divide big problem into smaller recursive bits
2. Find the base condition with simple answer
3. Return or roll back answer for base condition to solve all sub problems

Find the sum of all numbers between 1 and n
Iterative approach
```
def find_sum(n):
	sum = 0
	for i in range(1, n+1):
		sum += i
	return sum

if __name__ == "__main__":
	print(find_sum(5))
```

Recursive approach
```
def find_sum(n):
	if n == 1:
		return 1
	return n + find_sum(n-1)

if __name__ == "__main__":
	print(find_sum(5))

```

Fibonacci
```
def fib(n):
	if n == 0:
		return 0
	if n == 1:
		return 1
	return fib(n-1) + fib(n-2)
	
print(fib(4))
```

### Binary Search
Linear search is O(n)
Binary search only works with a sorted list, O(log(n))

Implement linear search iteratively:
```
def linear_search(list, num_find):
    for index, element in enumerate(list):
        if element == num_find:
            return index
    return -1

list = [1,2,3,4,5]
print(linear_search(list, 4))
```

Implement binary search iteratively:
```
def binary_search(list, num_find):
    left_index = 0
    right_index = len(list) - 1
    mid_index = 0

    while left_index <= right_index:
        mid_index = (left_index + right_index) // 2
        mid_num = list[mid_index]

        if num_find == mid_num:
            return mid_index
        
        elif mid_num < num_find:
            left_index = mid_index+1

        else:
            right_index = mid_index-1
    
    return -1

list = [1,2,3,4,5]
print(binary_search(list, 2))
```

Implement binary search recursively:
```
def binary_search_re(list, num_find, left_idx, right_idx):
    if left_idx > right_idx:
        return ("Invalid indexes")
    
    mid_index = (left_idx + right_idx) // 2
    mid_num = list[mid_index]
    if num_find == mid_num:
        return mid_index
        
    elif mid_num < num_find:
        left_idx = mid_index+1

    else:
        right_idx = mid_index-1
    
    return binary_search_re(list, num_find, left_idx, right_idx)

print(binary_search_re(list, 2, 0, len(list)-1))
```

### Two Pointers
Basic structure:
```
l = 0
r = len(arr)
while l<r:
	# shift pointers until arriving at some state
```

Sliding window:
```
l = 0
r = l + i
while r<len(arr)-1:
	# shift pointers until some state
```
### Tries

```
class TrieNode:
    def __init__(self):
        self.children = [None] * 26
        self.isLeaf = False
class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word: str) -> None:
        current = self.root 
        for letter in word:
            index = ord(letter) - ord('a')
            if not current.children[index]:
                current.children[index] = TrieNode()
            current = current.children[index]
        current.isLeaf = True
    
    def search(self, word: str) -> bool:
        current = self.root 
        for letter in word:
            index = ord(letter) - ord('a')
            if not current.children[index]:
                return False 
            current = current.children[index]
        return current.isLeaf and current
    
    def startsWith(self, prefix: str) -> bool:
        current = self.root 
        for letter in prefix:
            index = ord(letter) - ord('a')
            if not current.children[index]:
                return False
            current = current.children[index]
        return True
```