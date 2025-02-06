---
tags:
  - oop
  - "#python"
  - abstractbaseclass
  - descriptors
  - inheritance
  - interfaces
  - iterators
  - operatoroverloading
---
## Fundamentals of OOP
### Defining a class
- Define a class with the **class** keyword
- **__init__** is known as a constructor, and is called when a new class is created and takes *self* as the 1st parameter along with other parameters that will be passed into the class.
- *self* refers to the current instance of a class.

```python
class Person:
	def __init__(self, name, age):
		self.name = name
		self. age = age
		self.height = 0

# this invokes a call to __init__
john = Person("John Casey", 38)
```
### Instance attributes
- associated with an object of a class
- can be set and retrieved with syntax **self.\<attribute-name\>**
- accessed via **\<object-name\>.\<attribute-name\>

```python
class Person:
	def __init__(self, name, age):
		self.name = name
		self. age = age

# Create an instance of Person
sarah = Person("Sarah Walker", 31)

# Retrieve the age instance attribute
sarah.age 
```
### Class attributes
- tied to class itself.
- can be retrieved without an object of the class.
- can be retrieved with syntax: **\<class-name\>.\<attribute-name\>**
- store data that should be same for all class objects.
```python
class Person:
	residence = "Planet Earth"
	...

# Accessed without an instance
print(Person.residence)

#ouput: Planet Earth
```
### Methods
#### Instance methods
- require an object of a class to exist in order to be called.
- takes *self* as their first parameter, allowing them to access their other instance methods and attributes.

```python
# introduce is defined as instance method.
class Person:
	...
	def introduce(self):
		print(f"Hellow, my name is {self.name}")

chuck = Person("Chuck", 32) # object of a class
chuck.introduce() # Called on Person object
```
#### Class methods
- defined using class method decorator (i.e, **@classmethod**)
- can't access instance methods or attributes, but can be called without needing a class object to exist **[ Do not require a class object to be called ]**.

```python
class Person:
	@classmethod
	def wake_up():
		print("Time to start your day!")

# calling a class method
Person.wake_up()
```

### Inheritance
- Inheritance allows for code to be reused between classes.
	- The child class inherits all the functionality of parent class.
	- can be thought of using an "**is-a**" relationship.
	- e.g: **Emplyoee** class (*child*) can inherit from **Person** class (*parent*) as: *Employee is a person* so it makes sense for **Employee to inherit Person**.
	- Once a class has been inherited, it can implement additional functionality such as new attributes or methods.

```python
class Person: # Parent class
	def __init__(self, name, age):
		self.name
		self.age = age
	def introduce(self):
		print(f"Hello, my name is {self.name}")

class Employee(Person): # child class
	def __init__(self, name, age, title):
		Person.__init__(self, name, age)
		self.title = title
	def change_position(self, new_title):
		self.title = new title
```

```python
ram = Employee ("Ram", 25, "Technician")
ram.introduce() # inherited from person
print(ram.title)

# output: 
# Hello, my name is Ram
# Technician

ram.change_position("Cashier")
print(ram.title)
# Cashier - Output
```
#### super()
- super() can be used instead of class name to instantiate  parent class in child class and it doesn't require *self* to be passed.

```python
class Employee(Person):
	def __init__(self, name, age, title):
		# uses name of parent class
		Person.__init__(self, name, age)
		
		self.title = title
	...

# using super()
class Employee(Person):
	def __init__(self, name, age, title):
		# super(), instead of class name
		super().__init__(name, age)
		
		self.title = title
	...
```
#### Overriding
- child implements a method that was inherited from parent in a new way.

```python
class Employee(Person):
	...
	def introduce(self):
		print(f"""My name is {self.name}, I am a {self.title}""")

ram = Employee("Ram", 25, "Technician")
ram.introduce()

# output - My name is Ram, I am a Technician.
```

###  Overloading python Operators
- customize behavior of python operators for a class
##### Overloading **\==** Operator

- Customize the functionality of **\==**
	- use the **__eq__()** magic method
	- takes self and other
	- returns a boolean value

```python
class Person:
	def __init__(self, name):
		self.name = name

	def __eq__(self, other):
		return self.name == other.name

bryce = Person("Bryce")
orion = Person ("Orion)
print(bryce == orion) # false
```
##### Overloading the **+** operator
- use the **__add__()** magic method to overload **+**
- *self* and *other* are passed to **__add__()**
- create a net *Team* object using the *team_members* for object being "added"

```python
class Team:
	def __init__(self, team_members):
	# team members is a list of names
		self.team_members = team_members
		
	def __add__(self, other):
		# Adding team objects creates a larger Team
		return Team(self.team_members + other.team_members)

# Create two team objects
rookies = Team(['ram', 'shyam'])
veterans = Team(['hari', 'krishna'])

# Attempt to add these two team together
dream_team = rookies + veterans
print(type(dream_team))
print(dream_team.team_members)
# output: 
# Team
# ['ram', 'shyam', 'hari', 'krishna']
```
- Using + to create a new type of object
	-  what if we want to create a *team* by combining *Employee* objects?
		- **__add__** is implemented in the *Employee* class
		- creates a new object of *Team* by creating a list of *Employee* names.
		- the result of adding two *Employee* objects is a single *Team*.

```python
class Team:
	def __init__(self, team_members):
		self.team_members = team_members

class Employee:
	def __init__(self, name, title):
		self.name = name
		self.title = title

	def __add__(self, other):
		# use the + operator to create a Team with the name of each employee
		return Team([self.name, other.name])

# Create two employee objects
ram = Employee("Ram", "Technical Specialist")
sita = Employee("Sita", "musician")

# now attempt to add these together to create a team
audio_team = ram + sita
print(type(audio_team))
print(audio_team.team_members)

# output
# Team
# ["Ram", "Sita"]
```
![[Operators for overloading.png]]

### Multiple Inheritance
- allows for a class to inherit the functionality of more than a single class.
- maintains an "is-a" relationship.
### Multilevel Inheritance
- Inherit a class which inherits from another class, becoming a grandchild.
- Maintain an "is-a" relationship

### Method resolution order (MRO)
- The order in which Python determines which method is used when parent and children implement a method with same name.
- Follow these rules to determine MRO
	- Children will be searched first
	- Parent classes will be searched left-to-right as they were defined in class statement.
- To find a Class's MRO, **.mro()** method and **__mro__** attribute can be used.

```python
class Intern(Employee, Student):
	...

# find the MRO for intern
print(Intern.mro())

# output - result is a list of class names, in order which python will search when executing a certain method.

# find MRO using __mro__
print(Intern.__mro__)
# output - return value will be Tuple but will maintain the same order the mro method returns.
```
![[Intermediate OOP 1.pdf]]

# Type Hints
- are optional tool that allow information, or "hints", about the type of an object to be added to code.
- help make code easier to read and troubleshoot.
- Adding type hints to your code, is one of the *best way to demonstrate enterprise-grade Python skills.*
- Type hints are not enforced by the interpreter i.e, actual type of object can in fact be different than what was originally hinted.
- To create type hints, we use:
	- Built-in type keywords
		- Use the syntax **variable: type**
		- can also type hint parameters in a function or method signature using same syntax.
		- To hint the return type of a function or method, we'll **use an arrow and the return type after the last parenthesis but before the colon.** if method or function returns None, we can hint this using None keyword.

```python
# Type hinting for declarative logic
name: str = "Ram"
student_id: int = 123456
tution_balance: float = 123.87

# Type hinting for function/method definations
def get_schedule(semester: str) -> dict:
	...

```
-  *typing* library
		- **typing** is a library used to provide tool to type hint
		- with classes such as *List*, *Dict*, *Tuple*
		- allows both  top-level objects to be hinted, as well as elements of those objects.
		- **typing** library includes a number of other classes used for type hinting, including *Any, Set, Iterator,* and *Callable.*
		- we can use almost any class to add type hints to our code.

```python
from typing import List, Dict

student_names: List[str] = ["Morgan", "Chuck", "Anna"]
student_gpas: Dict[str, float] = { "Casey":3.71, "Sarah": 4.0 }

class Student:
	...

ram: Student = Student("Ram", 34342, 13000)

```


# Descriptors
- Descriptors are objects used to regulate the way that an attribute is retrieved, set, or deleted.
## Creating *Descriptors* with **@property**
- 'getter', 'setter', 'deleter'
	- interacts with **self.\_ssn**, not *self.ssn*
		- *@property* decorator manages the relationship between self.ssn and self.\_ssn
	- **@\<attribute-name\>.setter**
		- its common to add logic to validate data quality or perform operations on other attributes in this method.
	- **@\<attribute-name\>.deleter**
		- executed when attempting to delete the attribute.
- Method names == name of attribute
- Descriptors may also be created with
	- **property()** function
	- **__get__()**, **__set__()**, **__delete__()**

```python
class Student:
	def __init__(self, name, ssn):
		self.name = name
		self.ssn = ssn # Does not need to include an underscore

	@property
	def ssn(self): # This is the "getter" method
		# method regulates the logic executed when the attribute is retrieved.
		return "XXX-XX-" + self._ssn[-4:]

	# This is setter method with name "ssn", and takes an updated attribute value.
	@ssn.setter 
	def ssn(self, new_ssn):
		if len(new_ssn) == 11:
			# Add thing such as data
			# validation, operations on other attributes, etc.
		self._ssn = new_ssn

	@ssn.deleter
	def ssn(self):
		raise AttributeError("Can't delete SSN")
```
- Descriptors in action
```python
shaw = Student ("Ram Shaw", "183-89-1473")
print(shaw.ssn) # access the ssn attribute
# output - XXX-XX-1473

shaw.ssn = "173-38-4382" # update Shaw's social security number
print(shaw.ssn) # XXX-XX-1473

del shaw.ssn # Attempt to delete the ssn attribute
# AttributeError: Can't delete SSN
```

# Customizing Attribute Access
if we try to access the attribute of an object which doesn't exist, then the program throws *AttributeError*. We can give a different message when such non-existing attribute of object is accessed using **__getattr__()**
- **__getattr__()** is executed when an attempt to reference any attribute outside of an object's namespace is made
	- object's namespace is a collection of attributes that are associated with that object.
	- it's a magic method, not called directly
	- takes a *name* parameter
	- Implements custom functionality, rather than raising an **AttributeError**.

```python
# Rest of class defination above

	def __getattr__(self, name):
		# implement logic here
		...
```
## Resolving the attribute error

```python
class Student:
	def __init__(self, student_name, major):
		self.student_name = student_name
		self.major = major

	def __getattr__(self, name):
		print(f"""{name} does not exist in this object's namespace, try setting a value for {name} first""")

ram.residence_hall

# Output: residence_hall does not exist in this object's namespace, try setting a value for residence_hall first.
```
- **__setattr__()**
	- is a magic method that is executed when a (new or existing) attribute is set or updated.
	- includes when an attribute is created within a constructor using **__init__()**.
	- takes *name* of attribute and *value*.
	- Leverages **__dict__** attribute of the object.
		- **__dict__** stores all the attributes of the object, can be used to retrieve and store data.
- Using **__setattr__()** allows powerful control over object's attribute.
	- all the attributes can be validated or transformed before being set.

```python
# Rest of the class defination above

	def __setattr__(self, name, value):
		# Implement logic here
		...

		# use __dict__ to create/update the attribute
		self.__dict__[name] = value
```
## Customizing attribute storage

```python
class Student:
	def __init__(self, student_name, major):
		self.student_name = student_name
		self.major = major

	def __setattr__(self, name, value):
		# if value is string, set the attribute using __dict__ attribute
		if isinstance(value, str):
			print(f"Setting {name} = {value}")
			self.__dict__[name] = value

		else: # otherwise, raise an exception nothing an incorrect data type
			raise Exception("Unexpected data type!")

# set an attribute using a value of type 'str'
ram.residence_hall = "Honors college south"
print(ram.residence_hall)
# output
# Setting residence_hall = Honors college south
# Honors college south

# set an attribute using value of type 'int'
ram.student_id = 123

# output: Exception: Unexpected data type!
```

## Using __getattr__ and __setattr__ together

```python
class Student:
	...
	def __getattr__(self, name):
		# Set the attribute with a placeholder
		self.__setattr__(name, None)
		return None

	def __setattr__(self, name, value):
		if value is None: # Print a message denoting a placeholder
			print(f"setting placeholder for {name}")

		self.__dict__[name] = value # Set the attribute
```
- when an attribute outside the object's namespace is accessed, that attribute is stored with the value *None* and *None* is also returned.
	- this creates a Placeholder value rather than raising an attribute error.
- if value of an attribute is None, *setattr* method prints a message, before storing the attribute-value pair using dict, regardless of value's type.

# Custom Iterators
## Iterators
- classes that allow for a collection of objects or data stream to be traversed, and return one item at a time.
- are similar to *list*'s, *tuple*'s but act differently.
- Iterators can be used for navigating or transforming an existing collection of data, and are commonly-used when generating new data, such as rolling dice.
- Iterators can be looped over using for-loops or the next function can be used to pull an iterator's next value.

```python
# collection
chuck = NameIterator("Charles Dickens")
for letter in chuck:
	print(letter)

# Data stream
fun_game = DiceGame(rolls = 3)
next(fun_game) # .. and so on
```
- for class to be considered an iterator, it must implement the iterator protocol.

### Iterator protocol
- consists of two magic methods:
	- **__iter__()**
		- returns an iterator, in this case, a reference to itself
		- *return self*
	- **__next__()**
		- returns the next value in the collection or data stream.
		- iteration, transformation, and generation takes place.
- both must be defined for a class to be considered iterator!

```python
class CoinFlips:
	def __init__(self, number_of_flips):
		self.number_of_flips = number_of_flips # Store the total number of flips
		self.counter = 0
	
	def __iter__(self):
		return self # Return a reference of the iterator

	# Flip the next coin, return the output
	def __next__(self):
		# only do this if the coin hasn't been flipped "number_of_flips" times.
		if self.counter < self.number_of_flips:
			self.counter += 1
			return random.choide(["H", "T"])

		# Signals the end of collections/data stream
		# prevents infinite loops while traversing an iterator and
		# easy to handle
		else: # Otherwise, stop execution with StopIteration
			raise StopIteration

# Example usage of iterator
three_flips = CoinFlips(3)

# flip the coin 3 times
next(three_flips)
next(three_flips)
next(three_flips)

# output
# H
# H
# T

# OR
for flip in three_flips:
	print(flip)
# to stop for loop, else part is added in **__next__**.

# OR
# Handling StopIteraion exceptions
while True:
	try:
		next(three_flips) # pull the next element of three_flips

	# catch a stop iteration exception
	except StopIteration:
		print("Completed all coin flips")
		break

```

![[Intermediate OOP 2.pdf]]

# Abstract Base Classes
Abstract base classes create a blueprint for classes by defining abstract methods that must be implemented by all children.
- ensures common behavior for a group of classes.
- To use abstract method, we use **@abstractmethod** decorator from **abc** module.
- Abstract base classes are only meant to be inherited, not instantiated.
- Not all methods in abstract base class must be abstract (concrete methods.)

```python
class School:
	# Do things such as enroll
	# and add a class
class MiddleSchool:
	# Play an instrument, join a club 
	# but must enroll and add course
class HighSchool:
	# Play a varsity sport, apply
	# for college, but must enroll 
	# and add courses 
```

## Creating an abstract base class
- inherit the **ABC** class in the **abc** module.
- only add *pass* to the abstract method as it is meant to be implemented later in the classes inherited from it
- Abstract base classes can contain more than one abstract methods.
- can also implement concrete methods.
	- these methods are inherited by any class implementing the abstract base class, rather than needing to provide their own definition of the method

- In example below, any class that inherits *School* must implement the *enroll()* method.
- in example, graduate concrete method prints short congratulation.

```python
from abc import ABC, abstractmethod

# Create an abstract base class that inherits from ABC
class School(ABC):
	@abstractmethod
	def enroll(self):
		# This method is implemented in classes that inherited from it
		pass

	# Concrete methods are inherited
	def graduate(self):
		print("Congrats on graduating.)

```
## Implementing abstract base class
- *HighSchool* must define an *enroll()* method.
- *TypeError* if *enroll()* is not defined.
- *HighSchool* inherits the *graduate()* method.
```python
class HighSchool(School):
	def enroll(self):
		print("Welcome to high school!")

# Create an instance of HighSchool
high_school = HighSchool()
high_school.enroll()
# OUTPUT: Welcome to high school!

high_school.graduate()
# OUTPUT: Congrats on graduating!
```
## Multiple abstract methods

```python
class School(ABC):
	@abstractmethod
	def enroll(self):
		pass

	@abstractmethod
	def add_course(self, course_name):
		pass

	def graduate(self):
		print("Congrats on graduating!")

# Two abstract method, enroll() and add_course()

class HighSchool(School):
	def __init__(self):
		self.courses = []

	# Implementing abstract method
	def enroll(self):
		print("Welcome to high school!")

	# Implementing abstract method
	def add_course(self, course_name):
		self.courses.append(course_name)
		print(f"You enrolled in {course_name}")
```
# Interfaces
A special kind of class made up of only abstract methods that create a contract with that classes that implement the interface.
- must define abstract methods
- if class doesn't define an abstract method present in the interface, the contract is not fulfilled.
- Abstract method provide skeleton of method definitions, only including the method name, parameters and pass keyword.
- Parameters in abstract method typically act as a guideline for all classes implementing the interface, but don't need to match exactly.
- Interfaces can be either formal or informal.
![[Interface definition structure.png]]
## Informal interfaces
- are created using duck typing.
- Duck typing is commonly-used phrase in programming that goes something like
> if it looks like a duck, and acts like a duck, it's probably a duck.

```python
class Course:
	def assign_homework(self, assignment_number, due_date):
		# Typically the pass keyword will be used when creating an interface 
		pass
	def grade_assignment(self, assignment_number):
		pass
```
- in this case, Course is the duck; an informal duck interface with two abstract methods.
### informal interfaces with duck typing

```python
class ProgrammingCourse:
	def __init__(self, course_name):
		self.course_name = course_name

	def assign_homework(self, due_date):
		# Some implementation of assign_homework here...
	def grade_assignment(self, assignment_number):
		# Some implementation of grade_assignment here...
```
- ProgrammingCourse class informally fulfills the contract set out by the Course interface, without even inheriting the Course class.
- However this contract is not actually enforced in any way.
- to do this, formal interfaces are used

## Formal interfaces with ABC, @abstractmethod
- Formal interfaces are defined like abstract base classes, using the ABC class and abstract method decorator.

```python
from abc import ABC, abstractmethod

class Course(ABC):
	@abstractmethod
	def assign_homework(self, assignment_number, due_date):
		pass

	@abstractmethod
	def grade_assignment(self, assignment_number):
		pass
```
# Interfaces vs. Abstract Base Classes
| Interfaces                                                                           | Abstract base classes                                                      |
| ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| - Define a "contract" with classes that implement it via                             | - Create a "blueprint" for classes with common characteristics.            |
| - "must-do" relationship                                                             | - "is-a" relationship.                                                     |
| - Formal and Informal                                                                | Typically only formal                                                      |
| - can only contain abstract methods (no concrete methods.)                           | - Mix of abstract and concrete methods.                                    |
| - typically used to create nearly identical classes that can be easily interchanged. | - abstract base classes help to create classes that look and feel similar. |
- Like with abstract base classes, the class implementing a formal interface will inherit the interface itself.

```python
class ProgrammingCourse(Course):
	def __init__(self, course_name):
		self.course_name = course_name

	def assign_homework(self, due_date):
		# Some implementation of assign_homework here...
	def grade_assignment(self, assignment_number):
		# Some implementation of grade_assignment here...

intermediate_oop = ProgrammingCourse("Intermediate Object-Oriented Programming")
```

# Factory methods
- Factory method Design pattern uses factory methods to create objects that are used in another method.
- all object returned by factory method must implement the same interface.
- factory methods helps to reduce complexity in a method such as heavy conditional logic.
- They also make code more reusable and modular.
- use *\_* to denote the factory method

- as all factory methods must return objects which implement an interface. when working with factory methods, this interface is called a *product*.
- *Concrete Products* are the implementations of the product interface.
- These are the classes that will be instantiated and returned by a factory method.

```python
class Resource(ABC):
	@abstractmethod
	def reference(self, topic):
		pass

class Textbook(Resource):
	def __init__(self):
		self.index = {"Object-Oriented Programming": ['Inheritance', 'Constructors', ...]}

	def reference(self, topic):
		print(f"Referencing {topic} using a textbook")
		return self.index.get(topic)

	# something similar for blog, video
```

```python
class Student:
	# factory method to return Resource
	def _get_resource(self, resource_type):
		if resource_type == 'Textbook':
			return Textbook()

		elif resource_type == 'Blog':
			return Blog()

		elif resource_type == 'Video':
			return Video()

	def explore_topic(self, resource_type, topic):
		resource = self._get_resource(resource_type) # Retrieve the resource
		return resource.reference(topic)
```

```python
# Create a Student object, then have it reference a textbook
lester = Student()
lester.explore_topic("Textbook", "Object-oriented Programming")

# Each to swithc to another resource
lester.explore_topic("Video", "Object-oriented Programming")

# OUTPUT
# Referencing Object-oriented Programming using a textbook
# ["Inheritance", "Contructors", "Class-level methods"]

# Video are helpful for visual or audatory learners
# ["Classes", "Methods", "Attributes", "Self"]

```
![[example factory method..png]]!
![[Intermediate OOP 3.pdf]]


#operatoroverloading #factorymethod #abstractbaseclass #inheritance #descriptors #iterators
#interfaces #oop #python 