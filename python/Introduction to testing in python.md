**Testing** is a process of evaluating a system or software.
- needed to ensure that it meets specified requirements.
**Test** is a procedure to verify the correctness of a software application or system.

## Chapter One
#### Assert in Python
**assert condition** - lets to test if **condition** is **True**.
if **condition** is **False**, Python will raise an **AssertionError**.

### Testing with pytest
**pytest** - a popular testing framework in Python, which provides a simple way to write tests.

example of an "assert" test written with **pytest** in Python.
```python
import pytest

# A function to test
def squared(number):
	return number * number

# A test function always starts with "test"
def test_squared():
	assert squared(-2) == squared(2)
```

### Context Manager Recap
Context Manager - a Python object that is used by declaring a **with** statement.

we use **context managers** to set up and tear down temporary context

```python
with open("abc.txt", 'w') as abc:
	abc.write("hello, world \n")
```

**pytest.raises** - can be used when you expect the test to raise an **Exception**.

```python
import pytest

# A function to test
def division(a, b):
	return a / b

# A test function
def test_raises():
	with pytest.raises(ZeroDivisionError):
		division(a=25, b=0)
```

### Invoking pytest from Command Line Interface (CLI)

CLI - a user interface that allows to interact with a computer program by entering text commands into a terminal.

- CLI pytest command starts with ***pytest***.

#### Checking a single test script
```terminal
'if some tests are written in slides.py module'
pytest slides.py
```
Keyword **pytest** means we want to run the script using pytest framework (not just as a regular Python script.)

#### Checking a set of scripts from directory.
by passing *directory_name/*.
- writing */* after directory is not important but a good coding practice.
Tests are kept in **tests_dir/** directory for the following lines of code.

*FOR RUNNING ALL THE TESTS IN TESTS_DIR/:*
```terminal
pytest tests_dir/
```

TO RUN ONLY THE TESTS WITH CERTAIN NAMES - *FILTER TESTS BY NAME*
**-k** is for keyword argument.
```terminal
pytest tests_ex.py -k 'squared'
```
The above line of code means: 
run the **pytest** framework using all tests from the *tests_ex.py* script containing **squared**.

### Test Marker
- a tag (a marker)/attribute of a test in the *pytest* library.
- allows to specify behavior for particular tests by tagging them (marking them).
- *Decorator* - a design pattern in Python that allows a user to add new functionality to an existing object without modifying its structure.
- *Test markers syntax* are started with **\@pytest.mark** decorator:
- followed by another **dot(.)** and the marker name we want to use.
**\@pytest.mark.name_of_the_marker**
```python
import pytest

def get_length(string):
	return len(string)

# The test marker syntax
@pytest.mark.skip
def test_get_len():
	assert get_length('123') == 3
```
### Out-of-the-box implementations in pytest
#### Skip and skipif markers
- use **\@pytest.mark.skip** - when you want a test to be skipped in any case.

```python
import pytest

def get_length(string):
	return len(string)

# The test marker syntax
@pytest.mark.skip
def test_get_len():
	assert get_length('123') == 3
```
- use **\@pytest.mark.skipif** - if you want a test to be skipped if a given condition is **True**.

```python
import pytest

def get_length(string):
	return len(string)

# The skipif marker example
@pytest.mark.skipif('2 * 2 == 5')
def test_get_len():
	assert get_length('123') == 3
```
- use **\@pytest.mark.xfail** - when you expect a test to be failed.

```python
import pytest

def gen_sequence(n):
	return list(range(1, n+1))

# The xfail marker example
@pytest.mark.xfail
def test_gen_seq():
	assert gen_sequence(-1)
```
![[introduction to testing in python 1.pdf]]

## Chapter Two
### Introduction to fixture
Fixture - a prepared environment that can be used for a test execution.
Fixture setup - a process of preparing the environment and setting up resources that are required by one or more tests.

#### Why fixture?
- to make test setup easier.
- to isolate the test of the environment preparation.
- to make the fixture code reusable.

#### How to use fixtures?
![[implementing fixtures.png]]
#### fixture examples
![[fixture example.png]]![[fixture example 2.png]]

### Chain Fixture requests
Chain fixture request - a pytest feature, that allows a fixture to use another fixture.
- creates a composition of fixtures.
- Example use case: the steps of data pipeline.
![[chain_fixture_example_composition.png]]
#### why and when to use?
Chain fixtures request helps to:
- establish dependencies between fixtures.
- keep the code modular.
when useful?
- when we have several fixtures that depend on each other.
![[example of chain requests.png]]

#### How to use chain requests
- Prepare the program we want to test
- Prepare the testing functions
- Prepare the **pytest** fixtures
- Pass the fixture name to other fixture signature.

```python
@pytest.fixture
def process_data(setup_data):
	return setup_data.upper()

```

#### Fixture autouse
##### Autouse argument
- an optional boolean argument of a fixture.
- can be passed to the fixture decorator
- when **autouse=True**, the fixture function is executing regardless of a request
- helps to reduce the amount of redundant fixture calls
- usage: **\@pytest.fixture(autouse=True)**
##### When to use
in case we need to appy certain environment preparations or modifications.

**Note**
*we cannot declare variable inside a fixture function and use it outside by default.
With autouse, we can only change the variables which were declared outside of the fixture.*

##### usecase examples:
- reading and preparing for all tests
- configuring connections and environment parameters.
![[autouse example.png]]

##### Advantage of fixture autouse
- helps to reduce the number of redundant fixture calls, thus makes the code simpler.
#### Fixture Teardown
- a process of cleaning up ("tearing down") resources that were allocated or created using the setup of a testing environment.

##### why teardown?
- if not done may lead to:
	- Memory leaks
	- low speed of execution and performance issues.
	- invalid test results
	- Pipeline failures and errors.
##### When to use?
- when manipulating big objects which can lead to lack of memory.
- when more than one test use similar variable names.
- if *autouse* of fixture is used.
##### when not needed to use?
- if project includes only one script with one test.

##### Lazy evaluation in Python
*yield* - is a python keyword, which allows to create generators.

```python
# Example of generator function
def lazy_increment (n):
	for i in range(n):
		yield i
f = lazy_increment(5)
next(f) # 0
next(f) # 1
next(f) # 2
# each time function is called loop runs one time and yields corresponding number.
```
##### How to use teardown in Python?
- Replace *return* by *yield*.
- Place the teardown code after *yield*.
- Make sure that the setup code in only before *yield*.

##### Teardown example

```python
@pytest.fixture
def init_list():
	return []

@pytest.fixture(autouse= True)
def add_numbers_to_list(init_list):
	# Fixture setup
	init_list.extend([i for i in range(10)])
	# Fixture output
	yield init_list

	# Teardown statement
	init_list.clear()

def test_9(init_list):
	assert 9 in init_list
```
##### Advantages of Teardown
- prevents software failures.
- prevents potential drops of performance.

![[introduction to testing in python 2.pdf]]

## Chapter Three - Unit Testing with Python
#### Unit Test
- Unit - the smallest working part that can be tested. e.g: functions, methods, classes, modules, etc.
- Unit testing - software testing method.
	- unit testing allow one to scrutinize(examine or inspect) the correctness of a unit.
- Test Case - a set of unit inputs and expected outputs.
	- Test case summarizes a particular piece of the problem.
#### Why to use unit test?
- are foundation for testing 'the bigger picture' of the software.
- Use cases:
	- when bugs found
	- during development
	- after implemented changes
#### How to create Unit test
- Decide which units to test
- Define test cases ( the creative part):
	- what are possible unit outcomes?
	- how can one use the unit?
	- how should the unit behave in all those cases?
- write code for each test case
- Run the tests and analyze the results.

#### Creating a unit test: example
![[test case example1.png]]![[test case example 2.png]]

### Feature Testing with Pytest
#### Feature Test
##### Feature 
- a software system functionality.
- satisfies a particular user's requirement.
##### Features
- are wider than units
- end-user can use features.

##### Feature Testing
- software testing method
- verify the behavior of a specific feature.

##### Examples:
- Data distribution check
- Report preparation

#### Units vs. Features: Personal Computer
Units:
- each individual button
- pixels on the screen
- LED diodes
- Blocks on the disk

Features:
- Keyboard
- Screen
- Illumination
- File system

##### why to use feature tests
Feature testing helps
- to test things at the scope of the user interaction with a system.
- to ensure that user get exactly what they expect.
The Scope is wider than units:
- one unit doesn't work - doesn't mean the feature is NOT OK.
Vice Versa:
- All units work as expected - does not mean the feature is OK.

##### Feature testing example
![[feature testing example part 1.png]]
![[feature testing example part 2.png]]
To Create feature tests one has to create test cases.
Key to design feature tests - to understand what the features are in a specific system.

### Integration testing with pytest
- Integration test - software testing method, that allows to verify that an interaction behaves normally.
- integration - an interaction between 2 or more modules inside of a system.
- Real life integration examples
	- Power cable
	- internet connection
	- file reading driver
	- Application Programming interface (API) integration.
- Potential Integration Issues:
	- Lost connection
	- loss of data
	- interaction delays
	- low bandwidth
	- version conflicts
	- interface mismatch
	- others

``` python
'''
The idea of this test is to check that python can create a file and its being checked by method "os.path.exists"
if file exists, python could create it and integration works

'''
import pytest, os

@pytest.fixture
def setup_file():
	# crete temporary file
	file = 'test_file.txt'
	with open(file, "w") as f1:
		f1.write("Test data 1")
	yield file
	os.remove(file)
	
def test_fs(setup_file):
	file = setup_file
	# check that file was created successfully
	assert os.path.exists(file)
```
### Performance testing with pytest
- **Performance** - how efficiently does software utilizes the resources of the system to accomplish a task.
- i.e, performance is a number (or set of numbers) that describes the efficiency of some software
- **Performance testing** - is a type of testing that measures software performance.
| Resources | Cases |
|------------|--------|
| Execution time | website speed optimization |
|--|--|
| CPU | App receiving millions of request |
|--|--|
| RAM | Path planning for a robot vacuum |
|--|--|

#### Benchmark fixture
can be used by
- calling *benchmark* directly
- using **\@benchmark** as decorator
- The results describe the sample of measured runs in seconds.

```python
# installation
pip install pytest-benchmark

# example1.py
import time
def test_func(benchmark):
	benchmark(time.sleep, 1)

# CLI command
pytest example1.py

# example2.py
import time
def test_func(benchmark):
	@benchmark
	def sleep_for_1_sec():
		time.sleep(1)

# CLI Command
pytest example2.py
```

![[Introduction to testing in python 3.pdf]]

## Chapter four: Writing tests with Unit test
unittest - built-in Python framework for test automation (installed with python)
unittest - not only for unit tests alone
Based on OOP : each test case is a class, and each test is a method.
Test case: is an instance of testing.
Test suite - is a collection of test cases.

### unittest vs. pytest
Unitest:
- OOP-based -requires to create test classes
- built-in (installed with python)
- more assertion methods
pytest
- function based - searches for scripts and functions started with (*test_*)
- third party package (has to installed separately from *python* distribution)
- less assertion methods

### How to create a test with unittest
1. Declare a class inheriting from **unittest.TestCase**
2. Define test functions

```python
import unittest

# Declaring the TestCase class
'''It is important that declared class inherits from *unittest.TestCase* '''
class TestSquared (unittest.TestCase):
	# Defining the test
	def test_negative(self)
		self.assertEqual((-3) ** 2, 9)
```

### Assertion methods
- .assertEqual(), .assertNotEqual() - to check whether if some "A" is equal to some "b"
- .assertTrue(), .assertFalse() - to check truthfulness of some expression
- .assertIs(), .assertIsNone() - objects are equal with *assertIs* and that an object in "None" with *assertIsNone*.
- .assertIsInstance(), .assertIn() - *assertIsInstance* to check the object's type and *assertIn* to verify the object is present in a container (e.g: list)
- .assertRaises() - to check that the given exception is raised when the function is called.

### Running unittest CLI Interface
In the code below,
- *-m* is the module flag
- followed by *unittest* - **the name of module that we want to run**
- "test_sqneg.py" - name of the script
```terminal
python3 -m unittest test_sqneg.py

```
other flags
- Keyword argument: **unittest -k** - run test methods and classes that match the pattern or substring.

```terminal
python3 -m unitest -k "SomeStringOrPattern" test_script.py

eg: python3 -m k "squared" test_sqneg.py
```
- Fail Fast Flag: **unittest -f** - stop after test run on the first error or failure.

```terminal
python3 -m unittest -f test_script.py
```
- Catch flag: **unittest -c ** - lets to interrupt the test by pushing "Ctrl - C"
- if *Ctrl - C*
	- is pushed once, *unittest* waits for the current test to end and reports all the results so far.
	- is pushed twice, *unittest* raises *KeyboardInterrupt* exception.

```terminal
python3 -m unittest -c test_script.py
usecase example: when debugging a big test suite.
```
- Verbose flag: **unittest -v** - run tests with more detail

```terminal
python3 -m unittest -v test_script.py
usecase: debugging purposes
```

#### Fixtures in Unittest
- the preparation needed to perform one or more tests
- .setUp() - a method called to prepare the test fixture before the actual test
- .tearDown() - a method called after the test method to clean the environment.
- Correct syntax: **setUp with capital *"U"* and tearDown with capital *"D"* **

```python
import unittest

class TestLi(unittest.TestCase):
	# Fixture setup method
	def setUp(self):
		self.li = [i for i in range(100)]

	# Fixture teardown method
	def tearDown(self):
		self.li.clear()

	# Test method
	def test_your_list(self):
		self.assertIn(99, self.li)
```
Code Explanation:
	- python will execute all of the instructions inside of the 'setUp' method before running test function
	- then, python will execute all of test methods
	- finally, it will call the "tearDown" method to clean the environment.
	In the code above,
	- setup is initialization of list "li"
	- teardown is making the list empty by calling "clear" method.
	- test function uses "assert in" and "assert not in" to check the membership of certain elements in the list.

summary:
To create a fixture:
- implement the .setUp() method
- implement the .tearDown() method
- .setUp() - a method called to prepare the test fixture before the actual test.
- .tearDown() - a method called after the test method to clean the environment.

#Note: To delete a sting 'del' keyword can be used. e.g: del var_that_hold_sting, etc.
![[Proper test example.png]]
![[introduction to testing in python 4.pdf]]
