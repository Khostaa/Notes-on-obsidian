# importance of data structures and algorithms
- enable us to
	- solve everyday problems.
	- using efficient code.

# Algorithms
- set of instructions that solve a problem.
	- design
	- code
# Data Structures
- hold and manipulate data when we execute an algorithm.

## Linked lists
- sequence of data connected through links
- Each element is called node
- has two parts
	- Data
	- pointer to next node
- last link points to NULL.
- First node is called HEAD and last node is called TAIL.

- Data doesn't need to be stored in contiguous blocks of memory.
- Data can be located in any variable memory address.
- If each node has one link, *singly linked list*.
- if each node has two links in either direction, *doubly linked list*.

### Uses
- implement other data structures:
	- stacks
	- queues
	- graphs
- access information by navigating backward and forward.
	- web browser
	- music playlist
### Methods in linked list
- insert_at_beginning()
- insert_at_end()
- remove_at_beginning()
- remove_at_end()
- insert_at()
- remove_at()
- search()
- ...

```python
# Node class
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

# LinkedList class
class LinkedList:
	def __init__(self):
		self.head = None
		self.tail = None
```

```python
# Insert at beginning
def insert_at_beginning(self, data):
	new_node = Node(data)
	if self.head:
		new_node.next = self.head
		self.head = new_node
	else:
		self.tail = new_node
		self.head = new_node
```

```python
# insert at end
def insert_at_end(self, data):
	newnode = Node(data)
	if self.head:
		self.tail.next = new_node
		self.tail = new_node
	else:
		self.head = new_node
		self.tail = new_node
```

```python
# Search
def search(self, data):
	current_node = self.head
	while current_node:
		if current_node.data == data:
			return True
		else:
			current_node = current_node.next
	return False
```

```python
# example
sushi_prep = LinkedList()
sushi_prep.insert_at_end("Prepare")
sushi_prep.insert_at_end("roll")
sushi_prep.insert_at_beginning("assemble")

sushi_prep.search("roll") # True

sushi_prep.search("mixing") # False


```

# understanding Big O Notation
## Big O Notation
- Measures the *worst-case complexity* of an algorithm
	- **Time Complexity** : time taken to run completely
	- **Space complexity**: extra memory space
- *Mathematical expressions*: O(1), O(n), O($n^{2}$)
![[Big O graph.png]]
- increase in the input size of an algorithm increases the number of executed operations.
- For algorithms with a complexity of O of one, the number of operations remains constant even if input size changes.
- O(n) follows a linear path. The number of operations increases proportionally with increase in input.

- O of log n has logarithmic time complexity
- O($n^{2}$) is called quadratic time, and 
- O($n^{3}$), cubic time.
- The number of operations in these algorithms increases by a lot when we increase input.
![[big O of 1.png]]
![[o of n.png]]
![[o of nsquared.png]]
![[O of n cubed.png]]
![[calculating bit O notation.png]]
![[rules for simplifying big O notation.png]]
# Working with stacks
- LIFO - Last-In First-Out
	- last inserted item will be the first item to be removed.
- can only *add* at the *top*.
	- **pushing** onto the stack.
- can only *remove* from the *top*
	- **popping** from the stack.
- can only *read* the *last element*
	- **peeking** from the stack.

## Stacks - real uses
- Undo functionality
	- push each keystroke
	- pop last inserted keystroke
- Symbol checker:
	- push opening symbols
	- check closing symbol
	- pop matching opening symbol
- Function calls
	- push block of memory
	- pop after the execution ends

## Stacks - implementation using singly linked list
```python
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

class Stack:
	def __init__(self):
		self.top = None

# Pushing into stack
def push(self, data):
	new_node = Node(data)
	if self.top:
		new_node.next = self.top
	self.top = new_node

# Pop from TOS
def pop(self):
	if self.top is None:
		return None
	else:
		popped_node = self.top
		self.top = self.top.next
		popped_node.next = None
		return popped_node.data

def peek(self):
	if self.top:
		return self.top.data
	else:
		return None
```
## LifoQueue in Python
- python's queue module
- behaves like a stack

```python
import queue
my_book_stack = queue.LifoQueue(maxsize=0) # setting length of stack unlimited
my_book_stack.put("The misunderstading") # .put("ele") - to push into stack
my_book_stack.put("Persepolis")
my_book_stack.put("1984")

print("The size is: ", my_book_stack.qsize()) # .qsize() - to get size of stack

print(my_book_stack.get()) # .get() - to pop from TOS

print("Empty Stack:", my_book_stack.empty()) # .empty() to check if stack is empty

```
![[DSA in Python - Chapter 1.pdf]]

# Working with queues
## Queues
- FIFO: First-In First-Out
	- First inserted item is the first to be removed.
- Beginning: **head**
- Ending: **tail**
- *Enqueue* - can only insert at the end
- *Dequeue* - can only remove from the head
- Other kinds of queues:
	- Doubly ended queues
	- Circular queues
	- Priority queues
## Queues - real-world use cases use
- Printing tasks in a printer
	- Documents are printed in the order they are received.
- Applications where the *order of request matters*
	- Tickets for a concert
	- Taxi services

## Queues - implementation
```python
class Node:
	def __init__(self, data):
		self.data = data
		self.next = None

class Queue:
	def __init__(self):
		self.head = None
		self.tail = None


# Enqueuing the elements
def enqueue(self, data):
	new_node = Node(data)

	# if no elements
	if self.head == None:
		self.head = new_node
		self.tail = new_node
	else: # if elements already present
		self.tail.next = new_node
		self.tail = new_node

# Dequeuing the elements
def dequeue(self):
	if self.head:
		current_node = self.head
		self.head = current_node.next
		current_node.next = None

	if self.head == None: # if no elements in queue
		self.tail = None
```
## SimpleQueue in Python
### Module: queue
- Queue
- SimpleQueue
```python
import queue

orders_queue = queue.SimpleQueue()

orders_queue.put("Sushi")
orders_queue.put("Lasagna")
orders_queue.put("Paella")

print("The size is: ", orders_queue.qsize()) 
# The size is: 3

print(orders_queue.get()) # Sushi
print(orders_queue.get()) # Lasagna
print(orders_queue.get()) # Paella

print("Empty queue: ", orders_queue.empty())
# Empty queue: True
```
# Hash tables
- stores a collection of items
- Key-value pairs
- In python, hash table are implemented with dictionaries.
## Structure
- each position: **slot/bucket**
- When we create a hash table, every slot will be empty.
- When we add a new element to a hash table, there will be a mapping between the key and the slot where the value will be stored, using *hash functions.*
- Every time a hash function is applied, it needs to return the same value for the same input.
### Collisions
- Hash functions can return *same output* for *different inputs*.
- Collisions must be resolved and there're several techniques for them.

## Python hash tables
 - are called Python dictionary
```python
my_dict = {} # declaring empty dictionary

# dictionary with items - below: dishes are the keys and the prices are the values.
my_menu = {
		   'salad': 24,
		   'sushi': 20
}

# to get value from dictionary
print(my_menu['sushi']) # method one
print(my_menu.get('salad')) # method two

# Get items
print(my_menu.items())
# dict_items([('salad', 24),('sushi', 20)])

# Get keys
print(my_menu.keys())
# dict_keys(['salad', 'sushi'])

# Get values
print(my_menu.values())
# dict_values([24, 20])

# to insert new item
my_menu['samosas'] = 10

# modify the value of item
my_menu['sushi'] = 30

# Deletes a dictionary completely
del my_menu

# Removes a key-value pair
del my_menu['sushi']

# Empty a dictionary
my_menu.clear()
```
### iterating over dictionary
```python
# can iterate over a dictionary using a for loop over its items.
for key, value in my_men.items():
	print(f"\nkey: {key}")
	print(f"\nvalue: {value}")

# To access keys of each element
for dish in my_menu:
	print(dish)

# To access values of each element
for prices in my_menu.value():
	print(prices)
```

### nested dictionary
```python
my_menu = {
		   'sushi' : {
		   'price': 25,
		   'best_served' : 'cold'
		   },
		   'samosa' : {
		   'price': 10,
		   'best_served': 'hot'
		   }
}

# iterating over nested dictionary
for dish, values in my_menu.items():
	print(f"{dish.title()} is best served {values['best_served']}.")
```

# Trees and graphs
## Trees
 - node-based data structures
 - each node can have links to more than one node.
 - First node - root
 - a node can be a parent of other nodes called children.
 - Trees can have levels

### Binary trees
- trees with zero, one or two children

## Trees - real use
- storing hierarchical relationships
	- file system of a computer
	- structure of an HTML document
- chess: to store the possible moves of rival can make
- Searching and sorting algorithms

## Graphs
- A graph is a data structure formed by a set of nodes, also called vertices.
- nodes are connected by links, also called edges.
- Tress are type of graphs
### Graph types
- Directed graphs
	- have a specific direction
- Undirected graphs:
	- edges have no direction
	- the relationship is mutual
- weighted graphs
	- have numeric values associated with edges.
	- can be either directed or undirected.


| Trees                              | Graphs                            |
| ---------------------------------- | --------------------------------- |
| - cannot have cycles.              | - can have cycles.                |
| - all the nodes must be connected. | - there can be unconnected nodes. |
## Graphs - real world use-cases
- user relationships in social networks
	- friendship
	- follows
	- likes, etc.
 - Locations and distances
	 - optimize routes
- Graph databases
	- use graphs to store the information that is consumed by lots of applications.
- Searching and sorting algorithms.

```python
class Graph:
	def __init__(self):
		self.vertices = {} # a dictonary to store all the vertices

	def add_vertex(self, vertex): # method to add vertices
		self.vertices[vertex] = []

	def add_edge(self, source, target): # method to add edges
		self.vertices[source].append(target)
```

```python
my_graph = Graph()
my_graph.add_vertex("Sunil")
my_graph.add_vertex("Anil")
my_graph.add_vertex("Anita")

my_graph.add_edge('Sunil', 'Anil')
my_graph.add_edge('Anil', 'Anita')
my_graph.add_edge("Anita", "Sunil")

print(my_graph.vertices)
```
- we can also use adjacency matrices to print the vertices of graphs instead of .vertices

# Recursion
- function calling itself
- Almost all the situations where we use loops
	- substitute the loops using recursion
- recursion can solve problems that seem very complex at first

## Base case
- add a condition
	-  ensures that our algorithm doesn't execute forever.
	- doesn't need to make any recursive call in base case.

## How recursion works
- computer *uses a stack to keep track of the functions*
	- call stack

# Dynamic programming
- optimization technique
- mainly applied to recursion
- can reduce the complexity of recursive algorithms
- used for
	- any problem that can be divided into smaller subproblems the overlap
- solutions of subproblems are saved, avoiding the need to recalculate
	- can be done using *Memoization* technique.
```python
cache = [None] * (100)

def fibonacci(n):
	if n <= 1:
		return n

	 # check if value exists
	 if not cache[n]:
		 # save the result in cache
		 cache[n] = fibonacci(n-1) + fibonacci(n-2)
	return cache[n]

print(fibonacci(6)) # 8
```

![[DSA in Python - Chapter 2.pdf]]

# Linear Search and Binary Search
## Linear Search
- looping through each element
- Element found
	- algorithms stops
	- returns the result
- Element not found
	- algorithm continues
```python
def linear_search(unordered_list, search_value):
	for index in range(len(unordered_list)):
		if unordered_list[index] == search_value:
			return True
	return False

print(linear_search([15, 2, 21, 3, 12, 7, 8], 8)) # True
```
- has complexity: O(n)

## Binary Search
- only applies to ordered list
- compares *search_value* with the item in the middle of the list.
```python
def binary_search(ordered_list, search_value):
	first = 0
	last = len(ordered_list) - 1

	while first <= last:
		middle = (first + last) // 2
		if search_value == ordered_list[middle]:
			return True
		elif search_value < ordered_list[middle]:
			last = middle - 1
		else: 
			first = middle + 1
	return False
```
- Complexity: O(log n)
- O(log n ) is much better than the Linear search if the size of list is big.

## Binary search using recursion
```python
def binary_search_recursive(ordered_list, search_value):

# base case
	if len(ordered_list) == 0
		return False
	else:
		middle = len(ordered_list) // 2
		# check whether the search value equals the value in middle
		if search_value == ordered_list[middle]:
			return True
		elif search_value < ordered_list[middle]:
			# call recursively with the left half of the list
			return binary_search_recursive(ordered_list[:middle], search_value)
		else:
			# call recursively with the right half of the list
			return binary_search_recursive(ordere_list[middle+1:], search_value)

print(binary_search_recursive([1, 5, 8, 9, 16, 20, 50, 70, 72], 5)) # True
			
```

## Binary Search Tree (BST)
- Left subtree of a node:
	- values less than the node itself
- Right subtree of  a node:
	- values greater than the node itself
- Left and right subtrees must be binary search trees
### Implementation
```python
class TreeNode:
	def __init__(self, data, left=None, right= None):
		self.data = data
		self.left_child = left
		self.right_child = right

class BinarySearchTree:
	def __init__(self):
		self.root = None
```
### Searching
```python
def search(self, search_value):
	current_node = self.root
	while current_node:
		if search_value == current_node.data:
			return True
		elif search_value < current_node.data:
			current_node = current_node.left_child
		else:
			current_node = current_node.right_child
	return False
```
### Inserting
```python
def insert(self, data):
	new_node = TreeNode(data)
	if self.root == None: # no element in root node
		self.root = new_node
		return
	else:
		current_node = self.root
		while True:
			if data < current_node.data:
				if current_node.left_child == None:
					current_node.left_child = new_node
					return
				else:
					current_node = current_node.left_child
			elif data > current_node.data:
				if current_node.right_child == None:
					current_node.right_child = new_node
					return
				else:
					current_node = current_node.right_child
```
### Deleting
#### No children
- delete it

#### One child
- delete it
- connect the child with node's parent

#### Two children
- Two children
	- replace it with its successor
		- the node with the least value greater than value of the node
	- find the successor:
		- visit the right child
		- keep visiting the left nodes until the end
		- if the successor has a right child
			- child becomes the left child of successor's parent

### Uses of BST
- order lists efficiently
- Much faster at searching than arrays and linked lists
- Much faster at inserting and deleting than arrays
- used to implement more advanced data structures:
	- dynamic sets
	- lookup tables
	- priority queues

# Tree/graph traversal
- process of visiting all nodes
- can be performed with
	- Depth first Search (DFS)
	- Breadth first Search (BFS)

## Depth first search (DFS) - Trees
- In-order traversal
- pre-order traversal
- post-order traversal

### In-order traversal
order: **left -> current -> right**
- if applied to BST, yields the output is in ascending order
```python
def in_order(self, current_node):
	if current_node:
		self.in_order(current_node.left_child)
		print(current_node.data)
		self.in_order(current_node.right_child)

my_tree.in_order(my_tree.root)
```
- Complexity: O(n)
	- n -> number of nodes

### Pre-order traversal
order: **current -> left -> Right**
```python
def pre_order(self, current_node):
	if current_node:
		print(current_node.data)
		self.pre_order(current_node.left_child)
		self.pre_order(current_node.right_child)

my_tree.pre_order(my_tree.root)
```
### Post order traversal
Order: **Left -> Right -> Current**

### When to use in-order, pre-order and post-order
- in-order
	- used BST to obtain the node's value in ascending order
- pre-order
	- create copies of a tree
	- get prefix expressions
- post-order
	- delete binary trees
	- get postfix expressions

## DFS - graphs
- Graphs can have cycles
	- need to keep track of visited vertices
- steps:
	- start at any vertex
	- tracks current vertex to visited vertices list
	- for each current node's adjacent vertex
		- if it has visited -> ignore it
		- if it hasn't been visited -> recursively perform DFS
```python
def dfs(visited_vertices, graph, current_vertex):
	if current_vertex not in visited_vertices:
		print(current_vertex)
		visited_vertices.add(current_vertex)
		for adjacent_vertex in graph[current_vertex]:
			dfs(visited_vertices, graph, adjacent_vertex)
```
- Complexity: O(V + E)
	- V -> number of vertices
	- E -> number of edges

## Breadth First Search (BFS) - Trees
- starts for the root 
- visits every node of every level
```python
def bfs(self):
	if self.root:
		visited_nodes = []
		bfs_queue = queue.SimpleQueue()
		bfs_queue.put(self.root)
		while not bfs_queue.empty():
			current_node = bfs_queue.get()
			visited_nodes.append(current_node.data)
			if current_node.left:
				bfs_queue.put(current_node.left)
			if current_node.right:
				bfs_queue.put(current_node.right)
	return visited_nodes
```
- Complexity: O(n)
	- where 'n' - no. of nodes

## BFS - graphs
- Graphs can have cycles
	-  need to check if vertices have already been visited.
```python

def bfs(graph, initial_vertex):
	visited_vertex = []
	bfs_queue = queue.SimpleQueue()
	bfs_queue.put(initial_vertex)
	visited_vertices.append(initial_vertex)
	while not bfs_queue.empty():
		current_vertex = bfs_queue.get()
		for adjacent_vertex in graph[current_vertex]:
			if adjacent_vertex not in visited_vertices:
				visited_vertices.append(adjacent_vertex)
				bfs_queue.put(adjacent_vertex)
	return visited_vertices
```
- Complexity: O (V + E)
	- V -> no. of vertices
	- E -> no. of edges

| BFs                                        | DFS                                        |
| ------------------------------------------ | ------------------------------------------ |
| - Target close to the starting vertex      | - Target far away from the starting vertex |
| Applications:                              | Applications:                              |
| web crawling                               | solving puzzles with only one solution     |
| finding shortest path in unweighted graphs | Detecting cycles in graphs                 |
| finding connected locations using GPS      | Finding shortest path in a weighted graph  |
![[DSA in Python - Chapter 3.pdf]]

# Sorting algorithms
- solve how to sort an unsorted collection in ascending/descending order
- can reduce complexity of problems
- some sorting algorithms:
	- bubble sort
	- selection sort
	- merge sort
	- insertion sort
	- merge sort

## Bubble sort
- First value greater than the second value
	- Swap them
- Second value greater than the first value
	- Nothing
- Repeat till all elements are sorted.

### implementation 1 - normal
```python
def bubble_sort(my_list):
	list_length = len(my_list)
	for i in range(list_length - 1):
		# subtract i to avoid checking the already sorted values that are at the end of the list.
		 for j in range(list_length - 1 - i):
			 if my_list[j] > my_list[j+1]: # Comparing
				 my_list[j], my_list[j+1] = my_list[j+1], my_list[j] # swapping
	return my_list
```
### implementation 2 - improved
```python
def bubble_sort(my_list):
	list_length = len(my_list)
	is_sorted = False
	while not is_sorted:
		is_sorted = True
		for i in range(list_length - 1):
			if my_list[i] > my_list[i+1]:
				my_list[i], my_list[i+1] = my_list[i+1], my_list[i]
				is_sorted = False
		list_length -= 1
	return my_list
```

### Bubble sort - complexity
- worst case: O($n^{2}$)
- Best case - not improved version: $\Omega (n^{2})$
- Best case - improved version: $\Omega(n)$
- Average case: $\Theta(n^{2})$
- Doesn't perform well with highly unsorted large lists
- Peforms well:
	- large sorted/almost sorted lists
	- small lists
- Big Omega notation is used to indicate the complexity of the best case of an algorithm.
- Average case: expressed with Big Theta notation.

## Selection Sort
- determine the lowest value
- swap the lowest value with the first unordered element
- continue this until all the elements are sorted.
```python
def selection_sort(my_list):
	list_length = len(my_list)
	for i in range(list_length - 1):
		lowest = my_list[i]
		index = i
		for j in range(i+1, list_length):
			if my_list[j] < lowest:
				index = j
				lowest = my_list[j]
		my_list[i], my_list[index] = my_list[index], my_list[i]
	return my_list
	
```
### Selection sort - complexity
- Worst case: $O(n^{2})$
- Average case: $\Theta(n^{2})$
- Best case: $\Omega(n^{2})$

## Insertion sort
- compare the current element with each element before it and place it at first of the list, if it is the smallest/accordingly.
```python
def insertion_sort(my_list):
	for i in range(1, len(my_list)):
		number_to_order = my_list[i]
		j = i - 1
		while j >= 0 and number_to_order < my_list[j]:
			my_list[j + 1] = my_list[j]
			j -= 1
		my_list[j+1] = number_to_order
	return my_list
```

### Insertion sort - complexity
- Worst case: $O(n^{2})$
- Average case: $\Theta(n^{2})$
- Best case: $\Omega(n)$

## Merge sort
- follows the divide and conquer strategy
- Divide
	- divides the problem into smaller sub-problems
- Conquer
	- sub-problems are solved recursively
- Combine
	- solutions of sub-problems are combined to achieve the final solution

- Merge sort divides the data recursively into two parts and keeps dividing until each list has one element. then, combine them by sorting them into another list.


```python
def merge_sort(my_list):
	if len(my_list) > 1:
		mid = len(my_list)//2
		left_half = my_list[:mid]
		right_half = my_list[mid:]
		merge_sort(left_half)
		merge_sort(right_half)

	i = j = k = 0
	while i < len(left_half) and j < len(right_half):
		if left_half[i] < right_half[j]:
			my_list[k] = left_half[i]
			i += 1
		else:
			my_list[k] = right_half[j]
			j += 1
		k += 1
	while i < len(left_half):
		my_list[k] = left_half[i]
		i += 1
		k += 1

	while j < len(right_half):
		my_list[k] = right_half[j]
		j += 1
		k += 1

my_list = [35, 22, 90, 4 50, 20, 30, 40, 1]
merge_sort(my_list)
print(my_list)
```
### Merge sort - complexity
- worst case: $O(n\log n)$
- Average case: $\Theta(n \log n)$
- Best case: $\Omega(n log n)$
- Space complexity: O(n)
	- worst space complexity than others algorithms with O(1)
- other variants reduce this space complexity.

## Quicksort
- Follows divide and conquer principle.
- Implemented by many programming lanugages
- Partition technique
	- pivot
	- items smaller than the pivot -> left
	- items greater than the pivot -> right
- Elements to the left will be sorted recursively
- Elements to the right will be sorted recursively

- Hoare's partition
	-  set the pivot as the first element.
	- Move left pointer until a value greater than pivot is found
	- Move right pointer until a value lower than pivot is found.
### Implementation
```python
def quicksort(my_list, first_index, last_index):
	if first_index < last_index:
		partition_index = partition(my_list, first_index, last_index)
		quicksort(my_list, first_index, partition_index)
		quicksort(my_list, partition_index + 1, last_index)
```

```python
def partition(my_list, first_index, last_index):
	pivot = my_list[first_index]
	left_pointer = first_index + 1
	right_pointer = last_index

	while True:
		while my_list[left_pointer] < pivot and left_pointer < last_index:
			left_pointer += 1
		while my_list[right_pointer] > pivot and right_pointer >= first_index:
			right_pointer -= 1
		if left_pointer >= right_pointer:
			break
		my_list[left_pointer], my_list[right_pointer] = my_list[right_pointer], my_list[left_pointer]
	my_list[first_index], my_list[right_pointer] = my_list[right_pointer], my_list[first_index]
return right_pointer
```

```python
my_list = [6, 2, 9, 7, 4, 8]
quicksort(my_list, 0, len(my_list) - 1)
print(my_list) # [2, 4, 6, 7, 8, 9]
```
### Quicksort - complexity
- worst case: O($n^{2}$)
- very efficient!
	- Average case: $\Theta(n \log n)$
	- Best case: $\Omega(n log n)$
- Space complexity: O($n \log n$)

![[DSA in Python - Chapter 4.pdf]]
