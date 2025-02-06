- Minimal completion time (fast runtime)
- Minimal resource consumption (small memory footprint)
- "Follow the Zen of Python."
- "Pythonic Code == Efficient Code"

```python
# to look at the Zen of Python
import this
```
# Python Standard Library
- we should default to using a built-in solution (if one exists) rather than developing our own.
## Built-in types
- **list**, **tuple**, **set**, **dict** and others.
## Built-in functions
- '\*' character can be used to unpack the *range* and *enumerate* function.
- *print()*, *len()*, *range()*, *round()*, *enumerate()*, *map()*, *zip()* and others.
	- range(start, stop) 
	- range( start, stop, step)
	- range(stop)

```python
nums = range(6)

nums_list = list(nums)

# alternative
nums_list2 = [*range(6)]

# output
[1, 2, 3 ,4, 5]

```
-  enumerate()
		- creates a index item pair for each item in the object provided..
		- returns enumerate object
		- which can be converted into list and printed
		- enumerate ( list_to_enumerate, *start = index to start at (optional)*)

```python
letters = ['a', 'b', 'c']

indexed_letters = enumerate(letters)

indexed_letters_list = list(indexed_letters)
print(indexed_letters_list)

# Output
[(0, 'a'), (1, 'b'), (2, 'c')]
```
-  map(function_name, object_to_apply_that_function_on)
	- applies function over an object

```python
nums [ 1.5, 2.3, 3.4]

rnd_nums = map(round, nums)

print(list(rnd_nums))

# output
[2, 2, 3]
```
- map can also be used with *lambda* (anonymous function)
	- use map and  lambda expression to apply a function

```python
nums = [1, 2, 3]

sqrd_nums = map(lambda x: x ** 2, nums)

print(list(sqrd_nums))
```
## Built-in modules
- *os*, *sys*, *itertools*, *collections*, *math*, and others.

# The Power of NumPy arrays
- alternative to Python lists

```python
nums_list = list(range(5))
# output
[0, 1, 2, 3, 4]

import numpy as np
nums_np = np.array(range(5))

# output
array([0, 1, 2, 3, 4])
```
- np.array() - to create a numpy array
	- are homogeneous i.e, must contain elements of the same type.
	- To know type of each element **\.dtype**
	- Homogenetiy allow NumPy arrays to be more memory efficient and faster than Python lists.
		- all elements having same data type eliminates the overhead needed for data type checking.
## NumPy array broadcasting
- python list don't support broadcasting
```python
nums = [-2, -1, 0, 1, 2]

nums ** 2

# output
TypeError: ...

# This operation can be performed using loop or list comprehension but neither of these approaches is the most efficient way of doing this.
```
- NumPy array broadcasting for the win!
- NumPy arrays vectorize operations, so they are performed on all elements of an object at once
	- This allow us to efficiently perform calculations over entire arrays.
- NumPy arrays have indexing capabilities

```python
nums_np = np.array([-2, -1, 0, 1, 2])
nums_np ** 2

# output
array([4, 1, 0, 1, 4])
```

```python
# 2-D list
nums2 = [[1, 2, 3], [4, 5, 6]]

# basic 2-d indexing (lists)
nums2[0][1]
# To return first column values of 2-d list
[row[0] for row in num2]

# Output
2
[1, 4]
```

```python
# 2-D array
nums2_np = np.array(num2)

# Basic 2-D indexing (arrays)
nums2[0, 1]
# To return first column values in 2-d array
num2_np[:, 0]

# Output
2
array([1, 4])
```
## Boolean indexing in NumPy arrays

```python
nums = [ -2, -1, 0, 1, 2]
nums_np = np.array(nums)

# Boolean indexing
nums_np > 0
# output
array([False, False, False, True, True])

nums_np[nums_np > 0]
# output
array ([1, 2])
```
- Using NumPy array to index is less verbose and has a faster runtime.

# Examining runtime
- Runtime is an important consideration when thinking about efficiency.
- comparing runtime of the codes that does same thing, allows us to pick the code with the optimal performance.
- Faster code == more efficient code!
## How can we time our code?
- calculate runtime with IPython magic command *%timeit*
	- Magic commands: enhancements on top of normal python syntax.
		- Prefixed by "%" charater.
		- link to docs: ((https://ipython.readthedocs.io/en/stable/interactive/magics.html))
		- see all the magic commands with **%lsmagic**.

```python
import numpy as np
# code to be timed
rand_nums = np.random.rand(1000)
# Timing with %timeit
%timeit rand_nums = np.random.rand(1000)
```
- mean and standard deviation displayed in output is a summary of runtime considering each of the multiple runs.
- Setting the number of runs (**-r**) and/or loops (**-n**).

```python
# Set number of runs to 2 (-r2)
# Set number of loops to 10 (-n10)

%timeit -r2 -n10 rand_nums = np.random.rand(1000)
```
### using %timeit in line magic mode
Line magic (**%timeit**)

```python
# Single line of code

%timeit nums = [x for x in range(10)]
```
### Using %timeit in cell magic mode
Cell magic (%% timeit) - provide multiple lines of code by using two percentage signs.

```python
%%timeit
nums = []
for x in range(10):
	nums.append(x)
```
### Saving Output
- saving output to a variable (**-o**)
```python
times = %timeit -o rand_nums = np.random.rand(1000)

times.timings # gives time for each run.
times.best # gives best time for all runs.
times.worst # gives worst time for all runs.
```
### Comparing times
- using literal code instead of formal code is faster.

```python
# Formal declaration of dictionary
%timeit formal_dict = dict()

# Literal declaration of dictionary
%timeit literal_dict = {}
```

# Code Profiling
- Code profiling is a technique used to describe how long, and how often, various parts of a program are executed.
- beauty of code profiler is its ability to gather summary statistics[ Detailed stats on frequency and duration of function calls] on individual pieces of our code without using magic commands like **%timeit**
- Package used: **line_profiler**
	- to profile a function's runtime line-by-line.
```python
pip install line_profiler
```
- using **line_profiler** package

```python
%load_ext line_profiler
```
- Magic command for line-by-line times
```python
%lprun -f func_name func_name(args1, args2, ...)
```
- **-f** flag indicate  - profile a function
- Output - table that summarizes the profiling statistics.
- 1st Column - *Line* - displays line number
- 2nd column - *Hits* - displays no. of times the line was executed.
- 3rd column - *Time* - shows total amount of time each line took to execute.
	- *Timer Unit* at first line of o/p.
- 4th column - *Per Hit* - gives avg. amount of time spent executing a single line. [ calculated by dividing *time* column by *hits* column ]
- 5th column - *% Time* - shows percentage of time spent on a line relative to total amount of time spent in the function.
- 6th columns - *Line Contents* - source code is displayed for each line in Line Contents column.

***Note***: *%timeit* uses multiple loops in order to calculate an average and standard deviation 

## Code Profiling for memory usage

### Quick and dirty approach
- to calculate size of an individual object

```python
import sys
nums_list = [*range(1000)]

sys.getsizeof(nums_list)
```

### Code Profiling: memory
- Code profiling to analyze the memory allocation for each line of code in code base.
- Line-by-line analyses
- Package used: **memory_profiler**
```python
pip install memory_profiler
```
- Using **memory_profiler** package
```python
%load_ext memory_profiler

%mprun -f func_name func_name(args1, args2, ...)
```
- Functions must be imported when using **memory_profiler**
e.g: *convert_units* function is defined in **hero_funcs.py**
then,

```python
from hero_funcs import convert_units

%load_ext memory_profiler
%mprun -f convert_units convert_units(heroes, hts, wts)
```
Output details
- 1st column - Line no - represents the line number of code that has been profiled.
- 2nd column - Memory usage - is the memory used after that line has been executed.
- 3rd column - shows the difference in memory of the current line with respect to previous one. - this shows impact of current line on total memory usage.
- last column - *Line Contents* - shows source code that has been profiled.
- Profiling a function with *mprun* allows us to see what lines are taking up a large amount of memory and possibly develop a more efficient solution.
- **MiB** - mebibyte; 1 Mebibyte not equal to 1 Mega byte but can be asssumed that they are close enough to mean the same thing.

#### %mprun output caveats/warnings
- data must be large
- small memory allocations could result in **0.0 MiB** output.
	- i.e, small memory allocation may not show up when using %mprun and that is perfectly fine result.
- inspects memory by quering the operating system.
	- so this might be slightly different from the amount of memory that is actually used by Python interpreter.
	- so, results may differ between platforms and runs
		- can still observer how each line of code compares to others based on memory consumption.
#  Combining, Counting and iterating over objects efficiently
## Combining objects with zip

```python
names = ['a', 'b', 'c']
hps = [ 2, 3, 5]

combined_zip = zip(names, hps)
print(type(combined_zip)) 
# output: <class 'zip'>

# zip must be unpacked into list and printed to see the contents.
combined_zip_list = [*combined_zip]
print(combined_zip_list)
# output
# each item is a tuple of elements from the original lists.
[('a', 2), ('b', 3), ('c', 5)]
```
![[collections module.png]]
### Dictionary approach
![[counting with loops.png]]
### Collections - Counter approach
![[collections - counter.png]]
Checking runtime: Using Counter takes half the run time as the standard dictionary approach

## Itertools module
![[itertools.png]]
### Combinations with loop
![[combining with loop.png]]
### itertools module - combination
![[combinations from module.png]]
Comparing runtimes: Combinations is significantly faster than using iterating for loops.

## Set theory
**set** datatype in python has following methods:
- intersection(): all elements that are in both sets
- difference(): all elements in one set but not the other
- symmetric_difference(): all elements in exactly one set
- union(): all elements that are in either set.

- Fast Membership testing
	- Check if a value exists in a sequence or not
	- Using the **in** operator.

```python
list_a = ['Bulbasaur', 'Charmander', 'Squirtle']
list_b = ['Caterpie, 'Pidgey', 'Squirtle']

# Convert sets into list
set_a = set(list_a)
set_b = set(list_b)

set_a.intersection(set_b) # output: {'Squirtle'}	

set_a.difference(set_b) # {'Bulbasaur', 'Charmander'}
set_b.difference(set_a) # {'Caterpie', 'Pidgey'}

set_a.symmetric_difference(set_b) # {'Bulbasaur', 'Charmander', 'Caterpie', 'Pidgey'}

set_a.union(set_b) # {'Bulbasaur', 'Caterpie', 'Charmander', 'Pidgey', 'Squirtle'}
```
- Using Set is much faster approach.
#### Uniques with sets

```python
primary_types = ['a', 'b', 'c', 'd', ...]

unique_types_set = set(primary_types) # converts all unique elements of 'primary_types' list into set.

print(unique_types_set)
```

```python
# Checking if 'a' in present in list or set
print('a' in list_a)
print('a' in set_a)
```
# Eliminating loops
## Looping in Python
- Looping Patterns
	- **for** loop: iterate over sequence piece-by-piece.
	- **while** loop: repeat loop as long as condition is met.
	- "nested" loops: use one loop inside another loop.
- Benefits of eliminating loops
	- Fewer lines of code
	- Better code readability
		- flat is better than nested
	- Efficiency gains
- Alternatives
	- List Comprehension
	- Built-in map() function
	- built-in modules
	- NumPy 
## Writing better loops
- Understand what is being done with each loop iteration.
- Move one-time calculations outside (above) the loop.
- Use holistic conversions outside (below) the loop.
- Anything that can be done **once** should be outside the loop.

# Intro to Pandas DataFrame iteration.
## iterating DataFrame with iloc
![[Dataframe with iloc.png]]
## iterating with .iterrows()
- each object returned from .iterrows() contain *index* of each row as 1st element, *data* of each row of pandas series as second element. or a **single variable** can be used to represent tuple given by .iterrows()
- returns each row's values as a 'pandas series'
- square brackets( [ ] ) can be used to access attributes.
![[Iterating DF with iterrows().png]]
#note: using .iterrows() takes roughly half the time that iloc takes to iterate over a dataframe.

## iterating with .itertuples()
- converts each select row into "named tuple" object
- 'dot(.)' must be used to reference attribute of named tuple
![[comparing methods iterrows and itertuples.png]]
![[accessing named tupel's attributes using dot operator.png]]
## Pandas alternative to looping
- pandas *.apply()* method
	- takes a function and applies it to a DataFrame
		- must specify an axis to apply (*0* for columns; *1* for rows)
	- can be used with anonymous functions (*lambda* functions)
Example:

```python
run_diffs_apply = baseball_df.apply(
									lambda row: calc_run_diff(row['RS'], row['RA']), axis = 1)
baseball_df['RD'] = run_diffs_apply
print(baseball_df)
```
- This approach is comparatively faster than using for loop & iterrows or itertuples.

## Optimal pandas iterating
- pandas is built on NumPy.
	- take advantage of NumPy array efficiencies.
- use power of vectorization i.e, NumPy arrays

```python
run_diffs_np = baseball_df['RS'].values - baseball_df['RA'].values
baseball_df['RD'] = run_diffs_np
print(baseball_df)
```
- This approach takes time in Microseconds while all other approaches takes time in milliseconds.