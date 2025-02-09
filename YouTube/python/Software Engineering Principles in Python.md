***Software Engineering Concepts***
- Modularity
- Documentation
- Testing
- Version Control & Git
we can write modular code in python by leveraging packages, classes, and methods.

### Introduction to packages and documentation

#### Python Package Index (PyPi)
- gives us an easy platform to leverage published packages.
- packages can be installed from *PyPi* using a tool called **pip**.

 **Pip** - recursive acronym called '*Pip installs Packages*'

#### Installing numpy using pip
```python
pip install numpy
```

#### Reading documentation with help()

```python
help ( whatever you want help with )
```

Including documentation for your packages, classes, and methods will make using your code much easier.


### Python Enhancement Protocol 8 (PEP 8)
- is a defacto style guide for Python code.
- lets us know how to format our code to be as readable as possible and to quote PEP 8, "**code is read much more often than it is written**"
- pycodestyle - can check code in multiple files at once and its outputs descriptions of the violations along with the information to let you know exactly where you need to go to fix the issue.

#### Using pycodestyle
```python
pip install pycodestyle

## using it
pycodestyle filename.py
```
pycodestyle outputs a human readable description of the PEP 8 violation and an error code.
![[output from pycodestyle.png]]

### To check multiple files for PEP 8 Compliance
- using **pycodestyle** 's ***StyleGuide***

```python
# importint needed packages
import pycodestyle

# Create a StyleGuide instance
style_checker = pycodestyle.StyleGuide()

# Run PEP 8 check on multiple files
result = style_checker.check_files(['file1.py', 'file2.py'])

# Print result of PEP 8 style check
print(result.messages)
```
Package Structure
a minimal python package consists of 2 elements: a directory and a python file.

- Directory
    - python file

-  name of the directory will be the name of the package
	- should have short, all-lowercase names.
	- use of underscores in package name is discouraged but can be used if it improves readability.
	- recommended to pick a name that conveys functionality of the package.
- python file should be named  **__init__.py**
	- this file lets python know directory we created is package.
	

```python
import my_package
help (my_package)
```

	- other filenames convention is same as package name.
	- these other files called **submodules** can be imported as

![[Notes/YouTube/python/Slides/software engineering principles wtih python/package_file_structure.png]]

```python
import my_package.sub_module_name
my_package.sub_module_name.function_name
```

```python
import my_package.utils

my_package.utils.function_inside_utils( parameters if any)
```

#### Import functionality with **__init__.py**

```python
# working in work_dir/my_package/__init__.py
# . notation before utils means relative import
from .utils import func_name

# this step is importing function in init file
```

```Python
# working in work_dir/my_script.py
import my_package
my_package.func_name( parameters if any)
```

#### Extending package structure
- while working with multiple submodules, you should import your package's key functionality in you init file to make it directly and easily accessible.
- less central functionality can be accessed by users through the longer submodules.

--- Packages can be built inside packages, called 'subpackages' and have same file structure as packages i.e, must include ***__init__.py*** file.

### Making your package portable
Two main steps to share a python package are creating **setup.py** and **requirements.txt**
-- These two pieces provide information on how to install your package and recreate its required environment.
-- These files list information about what dependencies you have used as well as allowing you to describe your package with additional metadata.
### Portable Package Structure
![[file_structure_for_portability.png]]

#### contents of requirements.txt
A requirement file shows how to recreate the environment needed to properly use your package.
includes:
- a list of python packages and optionally the version requirements for each package.
- no space between letters and inequalities.
working in **working_directory/requirements.txt**

```python
#needed packages/version


# if version not needed
matplotlib

# if version is important, use double equals or  mark a minimum version by using greater than or equal
numpy==1.15.4
pycodestyle>=2.4.0
```
Working with ***terminal***
```terminal
pip install -r requirements.txt
```
recreated its environment with requirements.txt

#### contents of setup.py
setup.py is what tells pip how to install our actual package.
- can be defined using setuptools
![[contents of setup.py file.png]]

Additionally, specifying where to install requirements from.
![[install requirements.txt.png]]after completing setup.py, package can be installed using pip inside the same directory as our package.

```terminal
pip install .
```

### Adding classes to a package
It is similar to adding setup.py

**__init__** builds an instance of class and it also accepts self as its first argument.

The following is a sample class and other can be defined on their own way but following PEP8 convention.
```python
# working in working_directory/my_package/my_class.py

class MyClass: # use CamelCase for class name
	# create a instance of MyClass
	def __init__(self, value):
		self.attribute = value

# working in working_directory/my_package/__init__.py
from .my_class import MyClass # import class from file into __init__.py for easy access

# working in working_directory/my_script.py

import my_package
# create a instance of MyClass
my_instance = my_package.MyClass (value = 'class attribute value')
# Print out class attribute value
print(my_instance.attribute)
```
#### Adding functionality to classes
According to PEP 8, **non-public methods should be named with single leading underscore.

### DRY - Don't Repeat Yourself Principle
 - Use Inheritance
 - Parent class can be inherited in child class by passing it as a argument to child class.
	 - remember to instantiate the parent class in **__init__**.
 - Attributes of parent class can be accessed through child class.
![[Inheritance in Python.png]]

### Documentation in Python
- Comments
		- used in inline/ at the end of the code.
		- comment should explain why the line is doing something rather than what the line is doing.
		- Comments are documentation for yourself and collaborators.
- Docstrings
		- Docstrings are for your users.
		- are what python outputs whenever a user calls help on your functions and classes.
	 - Anatomy of docstring
		 - first section -> functionality of what we're documenting.
		 - second section -> parameters and return value of function.
		 - last section -> example usage / expected output

```python
# to view docstring
help(function_name)
```
	![[Docstring example.png]]

### Readability counts
- important step to write a maintainable project is writing readable code.
- Guidelines to write a readable code: The Zen of Python

```python
# to view zen of python
import this
```
- Descriptive naming
- Keep it simple
	- a function should do only one thing.

### Unit Testing
#### why testing?
- confirm code is working as intended.
- ensure changes in one function don't break another.
- protect against changes in a dependency.

#### Testing in python
1. doctest
		for smaller examples.
```python
import doctest
doctest.testmod()
```
2. pytest
		for larger cases.
		- files name start with test_...py
		- 

### Additional Tools
1. Sphinx - Generate beautiful documentation
2. Travis CI - Continuously test your code
3. GitHub & GitLab - Host your projects with git
4. Codecov - Discover where to improve your project tests
5. Code Climate - Analyze your code for improvements in readabillity.

![[Software Engg. with python 1.pdf]]
![[Software Engg. with python 2.pdf]]
![[Software Engg. with python 3.pdf]]
![[Software Engg. with python 4.pdf]]
