# Starting a package.
## why packaging?
- to make your code easier to reuse.
- to avoid lots of copying and pasting.
- to keep your functions up to date.
- to give your code to others.

## Scripts, Modules and packages
- Script - A python file which is run like *python myscript.py*.
- Package - a directory full of python code to be imported.
	- e.g: numpy.
- Subpackage - A smaller package inside a package
	- e.g: numpy.random and numpy.linalg
- Module - A python file inside a package which stores the package code.
- Library - Either a package, or collections of packages.
	- e.g: the python standard library (*math*, *os*, *datetime*, ...)

## Directory tree of package
> mysimplepackage/
> |-- simplemodule.py
> |-- \_\_init__.py

- this directory, called *mysimplepackage*, is a python package.
- *simplemodule.py* contains all the package code.
- *\__init__.py* marks this directory as a python package.

## Directory tree for packages with subpackages.
![[Directory tree for package with subpackages..png]]
# Documentation
why documentation?
- helps your users use your code.
- Document each
	- Function
	- Class 
	- Class method
- can be accessed using **help( keywords to get help for)**
## Function documentation

```python
def count_words(args1, args2):
 """ Count the total number of times these words appear. 
 
 [explain what filepath and words_list are]

[what is returned]
 
 """

```
## Documentation style
- several standards but *style* must be consistent within the package.
### NumPy documentation style

```python
def func(arg1, arg2, arg3):
	"""
	[describe what function does]

	[write what function returns]

	Parameters
	----------
	arg1: *datatype*
		describe the parameter1
	...
	arg2: {if multiple types for parameter possible, write by separating with comma}
	...
	arg3: {if multiple values are possible, specfiy those separated by comma as well}
	...
	Returns
	-------
	retdata: *datatype*
		describe returned 
	"""
```
- other sections that can be included in NumPy documentation style:
	- Raises
	- See Also
	- Notes
	- References
	- Examples
### Documentation templates and style translation
- *pyment* can be used to generate docstrings.
	- run from terminal
	- can generate documentation in any style
		- Google
		- Numpydoc
		- reST(i.e, reStructured-text)
		- Javadoc(i.e. epytext)

```terminal
pyment -w -o numpydoc filetogeneratetemplatein.py
```
- **-w** - overwrite file
- **-o numpydoc** - output in NumPy style

- Creates templates with headings and parameters names.
- Fill in rest of the detail afterward.

#### To translate from one documentation style from another

```Terminal
pyment -w -o google filetogeneratetemplatein.py
```
- this line of code translates NumPy documentation as created in above lines into Google documentation style.

## Package, subpackage and module documentation
- Package documentation is placed in a string at the top of package **__init__.py** file
in **__init__.py** file

```python
"""
Package name
-------------
-------------

this is how package is described in package documentation.
This should summarize the package
"""
```
- subpackage documentation is placed at the top of subpackage **__init__.py**
- module documentation is written at the top of the module file.

# Structuring imports
## Directory tree for package with subpackages
![[File structure for import.png]]
## Importing subpackages into packages
i.e, Import subpackages into packages **__init__** file so that package recognizes the existence of sub pacakge.
In **mysklearn/__init__.py**
### Absolute import

```python
from sklearn import preprocessing
```
- used more - more explictiy
### Relative import

```python
from . import preprocessing
```
- used sometimes - shorter and sometimes simpler

## Importing modules
- importing *normalize* module into *preprocessing* subpackage.
In **mysklearn/preprocessing/__init__.py**
### Absoute import

```python
from mysklearn.preprocessing import normalize
```
### Relative import

```python
from . import normalize
```

# Restructuring import
## import function into subpackage
- importing *normalize_data* function from *nomalize.py* module into subpackage *preprocessing*.
In **mysklearn/preprocessing/__init__.py**
### Absolute import

```python
from mysklearn.preprocessing.normalize import \ normzlize_data
```

### Relative import

```python
from .normalize import normalize_data
```

## importing between sibling modules
![[Notes/python/Developing Python packages/package_file_structure.png]]
- import *mymax*, *mymin* functions from *funcs.py* into *normalize.py*
### Absolute import

```python
from sklearn.preprocessing.funcs import ( mymax, mymin)
```
### Relative import

```python
from .funcs import mymax, mymin
```

## importing between modules far apart
A custom exception *MyException* is in *utils.py*
- In *normalize.py*, *standardize.py* and *regression.py*
### Absolute import

```python
from mysklearn.utils import MyException
```
### Relative import

```python
from ..utils import MyException
```

![[Relative import cheat sheet.png]]

![[Developing python packages 1.pdf]]
# Installing your own package
## setup.py
- used to install the package
- contains metadata on package.
![[file structure for package including setup.py.png]]
- make a outer directory name same as inner directory and create a *setup.py* file inside it.
### inside setup.py
- call the setup function.
- version number = (major-number).(minor-number).(patch-number)
	- increase patch-number for bug fixes, and improvements to the functions that already exists.
	- increase the minor number for new features.
	- increase the major number for really big changes.
- *find_packages* function is used  to find the paths of your packages and subpackages.

```python
# import required functions
from setuptools import setup, find_packages

# Call setup function
setup(
	  author="Sunil Paudel",
	  description= "A complete package for linear regression"
	  name="mysklearn",
	  version="0.1.0",
	  packages=find_packages(include=["mysklearn", "mysklearn.*"]),
)
```
- Find_packages function includes the my-sklearn package.
- my-sklearn.* tells the function to include all the subpackages inside my-sklearn as well.

## Editable package Installation
- navigate to directory containing the setup file
- then use pip to install the package

```python
pip install -e .
```
- pip runs *setup.py* file
- *.* = package in current directory.
- **-e** means to install this package in an editable mode.
	- this means when you make changes to the source code, like fixing a bug or adding new features, these changes are included when you import the package.
	- if you didn't do this, you would need to reinstall the package each time you make a change.

# Dealing with dependencies
## Dependencies
- other packages you import inside your package.
## Adding dependencies to setup.py file
```python
from setuptools import setup, find_packages

setup(
	...
	install_requires= ['numpy', 'scipy', 'matplotlib'] 
	# any version of these packages can work	
)
```
## controlling dependency version
- allow as many package versions as possible
- get rid of unused dependencies

```python
from setuptools import setup, find_packages

setup(
	  ...
	  install_requires=[
	  'pandas>=1.0', # good
	  'scipy==1.1'   # bad
	  'matplotlib>=2.2.1,<3' # good
	  
	  ]
)
```
## python versions
- python versions required can be specified.
```python
from setuptools import setup, find_packages

setup(
	  ...
	  python_requires= '>=2.7, !=3.0.*, !=3.1.*',
)
```
## Choosing dependency and package versions
- check the package history or release notes
- test different versions

## Making an environment for developers
![[File location of requirements text.png]]
- Show all the package versions you have installed using **pip freeze** command.
- You should export this information into a text file which you include with your package.
- Save package requirements to a file

```python
pip freeze > requirements.txt
```
- install requirements from file

```python
pip install -r requirements.txt
```
## Including licenses and writing READMEs
### Why do I need a license?
- To give others permission to use your code.
- if you host your code only and you do not include a license, then you are not giving permission to other people to share, modify or even use the code!
### Open source licenses

More info here: [Choosealicense](https://choosealicense.com/)
- allow users to
	- use your package.
	- modify your package.
	- distribute version of your package.

### what is a README?
- The 'front page' of your package.
- Displayed on GitHub or PyPI.

### what to include in a README
README sections
- Title
- Description and Features
	- Description of the package including its most important features.
- Installation
	- instructions on how to install the package.
- Usage example
	- some example uses to get started.
- Contributing
	- a section on how to contribute to the package code.
- License
	-  a brief not on the type of license used.

### README format
- Markdown (commonmark)
	- contained in *README.md* file
	- simpler
	- used in wild
- reStructuredText
	- Contained in *README.rst* file
	- more complex
	- also common in wild.

#### commonmark
Commonmark is a file format like HTML, but is much much simpler.

License, README file should be added to the top directory, alongside setup script and the requirements file.
![[File directory location for license and readmefile.png]]

## MANIFEST.in
- lists all the extra files to include in your package distribution.
![[Manifest in file structure.png]]

- contents of **MANIFEST.in**

```
include LICENSE
include README.md
```

# Publishing your package

## PyPI - Python Package Index
- **pip** installs packages from [here](https://pypi.org/)
- Anyone can upload packages
- You should upload your package as soon as it might be useful
- When you upload your package to PyPI, you actually upload a package distribution.
- when you upload your package to PyPI, it is good practice to upload both the wheel and the source distribution.
## Distributions
- Distribution package - a bundled version of your package which is ready to install.
### Types of Distributions
#### Source Distribution
- a distribution package which is mostly your source code.
- To install this distribution the files must be downloaded and then the setup script is run.
#### Wheel Distribution
- a distribution package which has been processed to make it faster to install.
- **Preferred Python Distribution** - pip will install this package when it is available.

### How to build distributions
![[Package File Structure.png]]
- To build source and wheel distributions from the terminal use the following command:
```terminal
python setup.py sdist bdist_wheel
```
- **sdist** = source distribution
- **bdist_wheel** = wheel distribution
![[Directory after building distributions.png]]

## Upload your package to PyPI
- First make a account in [PyPI](https://pypi.org/)
- Twine is a tool specially made for uploading packages to PyPI
```terminal
twine upload dist/*
```
- This code uploads all the distribution is dist directory to the PyPI.

## Upload your packages to TestPyPI
- First make an account in [Test-PyPI](https://test.pypi.org/)
- TestPyPI - version of PyPI repository made for testing
- good place to start

```terminal
twine upload -r testpypi dist/*
```

## How other people can install your package
- install from **PyPI**
```python
pip install package_name
```
- install from **TestPyPI**

```python
pip install --index-url  https://test.pypi.org/simple
			--extra-index-url https://pypi.org/simple
			mysklearn
```
- **index-url** - where the package is downloaded from
- **extra-index-url** - where PIP can search for you dependency packages
![[Developing python packages 2.pdf]]

# Testing your package
## The art and discipline of testing
- Good packages brag about how many tests they have

## Writing tests
- Each function in your package should have test function
```python
def get_ends(x):
	""" Get the first and last element in a list"""
	return x[0], x[1]

def test_get_ends(x):
	assert get_ends([1, 5, 39, 0]) == (1, 0)
```
In above test, if it doesn't pass the test, it raises assertion error.
## Organizing tests inside your package
![[tests inside package.png]]
![[test vs code directory layout.png]]
- The best way to lay out the tests directory is to copy the structure of the code directory. 
- The test directory has an empty init file and the preprocessing subdirectory. 
- Inside this subdirectory is the test-normalize module.
- The test-normalize module should contain all the tests for functions in the normalize module. 
- Every other module in the code directory should have its own test module in the test directory.
- Inside the test module, there should be a test function for each function defined in the source module.
- Remember that you will need to **import the functions** you are testing from the main package. This should be done **using an absolute import**.
![[Organizing test module.png]]
![[Running test with pytest.png]]

# Testing your package with different environments
## What is tox?
- Tox is a tool specifically built to run package tests with multiple versions of Python. You can run tox from the terminal, just like pytest.
![[Configuration file - tox placement in directory.png]]
```tox.ini
[tox]
envlist = py27, py35, py36, py37

[testenv]
deps = pytest
commands = 
	pytest
	echo "run more commands"
	...
```
- Inside the file you need to create the tox heading like this. 
- You will then specify the versions of Python you want to test using the envlist parameter. 
- Here we are testing python 2.7, 3.5, 3.6 and 3.7. You need to have these versions of Python already installed on your computer. Tox won't install new python versions. Using each of these versions of Python, tox will install your package and its dependencies. 
- Under the testenv heading you need to tell tox what you want it to do once it has installed your package.
- You use the commands parameter to tell tox to run pytest. However, pytest isn't installed by your package dependencies, so you need to specify pytest as a tox dependency.
- You could actually add any commands you like to the commands list and tox will run them all. These need to be shell commands, which you could run from the terminal
![[format to write in tox.ini file.png]]
- To run **tox**
	- navigate to top of directory.
	- type in **tox** in terminal.

# Keep your package stylish
## Introducing Flake8
- Standard Python style is described in *PEP8*.
- A style guide dictates how code should be laid out.
- Flake8 is a static code checker, which means it reads through your code without actually running through it.
- It prints a series of style improvement suggestions. The output includes the file name, then the line number, then the character number of the violation, and a problem code and description.

```python
flake8 features.py
```
- Remember that PEP8 is only a guide, so you might bend these rules occasionally.
-- Breaking the rule on purpose
- add ** #noqa ** comment on the line. This stands for no quality-assurance. Now, flake8 won't evaluate this line of code.
- If we include a violation code after **noqa**, then flake8 will evaluate the line but ignore this particular type of violation.

### flake8 settings
Ignoring style violations without using comments.
- It is possible to ignore specific errors using flake8 without adding comments. For the previous case, we could use flake8's ignore flag and pass it a list of violation codes to ignore. Or if we only want to search for a specific set of violations, we can select those. Here we search for unused imports and variables.
```python
...
quadratic_1 = 6 * x**2 + 2 * x + 4; # noqa: E222
quadratic_2 = 12 * x**2 + 2 * x + 8
...

# To run it via terminal
flake8 --ignore E222 quadratic.py

flake8 --select F401, F841 features.py
```
### Choosing package settings using setup.cfg
- Create a **setup.cfg** to store settings
![[creating setup.cfg.png]]
In this config file, we create a section header for flake8 and then define the settings we want. For example, we'll ignore line spacing in all modules, and we will exclude setup-dot-py from being evaluated. We can also tell flake8 to ignore specific violations in particular files. Here we tell it to ignore extra spaces, but only in the main module of this example package. When we use flake8 inside our package, these settings will be used without us having to specify them.

- You can run flake8 on the whole package at once by navigating to the top of the package, and running flake8 from the terminal.

```terminal
flake8
```
![[Filtering in Flake8.png]]
![[Developing python packages 3.pdf]]

# Faster package development with templates
## Templates
- Python packages have a lot of extra files.
- there is a lot to remember.
- using templates takes care of a lot of this
![[package file tree.png]]
## Cookiecutter
- Cookiecutter is a command line tool which creates projects from templates.
- can be used to create empty Python packages.
- creates all the additional files your package needs.
- cookiecutter creates a new directory with your package name, and fills it with all the files we have covered. Each of these files has good default content. Even the setup-dot-py file has been completely filled out. However, you may still want to make some edits.
- For more Package templates, click [here](https://cookiecutter.readthedocs.io/en/1.7.2/README.html#a-pantry-full-of-cookiecutters)
- 
### Using cookiecutter
```python
cookiecutter <template-url>
```

```python
# standard template for Python package is the following github link:
cookiecutter https://github.com/audreyr/cookiecutter-pypackage
```
- Fill in the details it requires
- Each field has a default value in square brackets.
- Press enter/return to continue
- It will prompt you for some more details used to fill in the template.
- The slug is just the name you want the package to registered under.
	- Project slug - the **name** used in **pip install name**
- Project description will go in README file. You can still manually edit the contents of README file later.
- specify yes to use pytest, and no to the other two options. We haven't been able to cover these in this course.
- We also don't use a command-line interface, so we enter 3 to pick this option. We will include an author file, which is just a list of the package authors
- Finally, you can choose a license, if one of the options is appropriate for you. If not, you can choose not-open-source and add a license manually.

# Version numbers and history
## CONTRIBUTING.md
- is either markdown or reStructured-Text file.
- invites other developers to work on your project.
- tells them how to get started.

## History.md
- History file is used to figure out which versions of a package will work with your package.
- different terms for this file - *history*, *change-log*, or *release notes*.
- The history file will tell your users the important things that have changed between the previous and new releases.
- This allows them to figure out which versions of your package they should use.
- The history file is also a markdown or restructured text file. There is no official guide on how to structure this file, but best practices would look something like this.
- Section for each release version
- Bullet points of the important changes.
- Subsections for 
	- improvements to existing functions
	- New additions
	- Bugs that have been fixed
	- Deprecations
![[History file probable structure.png]]
- Not all updates will be included here, just the ones which might affect your users.

## Version number
- increase version number when ready for new release.
- cannot upload to PyPI if not changed.
- Places where *version numbers* to be updated: 
-![[places where version number to be updated.png]]
	- Top level **\_\_init\_\_.py** file.
	- setup.py file
	- The version number in the setup file is used by pip and PyPI. 
	- The version number in the init file is included for the user, and it is best-practices to include this. It allows them to print and use the package version.
## bumpversion
- can be used to update the version numbers as mentioned above simulatenously using bump-version tool.
-  This tool is used from the terminal and will search through your package and increase the version number in appropriate places.
- navigate to the top of your package and run bump-version with the argument major, minor or patch, and it will increase the major, minor or patch number.
```python
# navige to the top of your package and use the following lines of code as required

bumpversion major

bumpversion minor

bumpversion patch
```
![[Navigate here to use bump version.png]]

# Makefiles and classifiers
- Makefiles will speed up your development.
- Classifiers will help people find your package.
## Classifiers
![[what's inside classifiers.png]]
- Inside the setup-dot-py file you will notice that cookiecutter has filled in the classifiers parameter. This is a list of categories for each release of your package. Users on PyPI can search through packages, and filter based on classifiers. Like if they are looking for packages for Python 2, or with a particular license type. Here we have classified that the mysklearn package is currently intended for developers, and is in pre-alpha stage, meaning it's not ready to be used by general users. We state the type of license, the language used in the package, and the versions of Python it is compatible with. This package is for Python 3, so we add this classifier. We also add classifiers for the minor versions 3.6 to 3.8, since these are the specific versions of Python 3 that the package works with. There are lots more classifiers you can use for your package, but you should always include these as a minimum. You can see a full list of classifiers [here](https://pypi.org/classifiers).

## Makefile
- are like Python modules
- you can write function inside them, but these functions are used from the terminal.
-  Inside the Makefile, cookiecutter has added a bunch of functions like this dist function. This function runs the setup-dot-py file to build source and wheel distributions for your package. There is also a clean-build function, which deletes the old distribution files so you can safely create new ones for a new release. There is also the test function, which simply runs pytest, and the release function which uploads your newest distributions to PyPI.
![[what's in a makefile.png]]
### How do I use Makefile?
- navigate to top of package
```terminal
make <function-name>
```
- to build new source and wheel distributions
```terminal
make dist
```
- get a summary of the commands available in the Makefile by using the make help command. This lists the functions in the makefile as well as what they do.
```terminal
make help
```
![[Developing python packages 4.pdf]]
#python #packagedevelopment #cookiecutter #pypi