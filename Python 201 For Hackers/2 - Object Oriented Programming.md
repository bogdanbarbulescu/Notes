
## Introduction

![[Pasted image 20230504170739.png]]

![[Pasted image 20230504171118.png]]

![[Pasted image 20230504171610.png]]

The main focus of the Python 201 for Hackers course is Python.

For more information related to the non-Python topics covered in this lesson, please refer to the following Wikipedia resource(s):

-   [https://en.wikipedia.org/wiki/Object-oriented_programming](https://en.wikipedia.org/wiki/Object-oriented_programming)


## Classes, Objects and Methods

```python
class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.age = age

	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.age))

	def birthday(self):
		self.age += 1


bob = Person("bob", 30)
alice = Person("alice", 20)
mallory = Person("mallory", 50)

print(bob)
print(alice)
print(mallory)

bob.print_name()
alice.print_name()
mallory.print_name()

bob.print_age()
alice.print_age()
mallory.print_age()

bob.age = 31
bob.print_age()

bob.birthday()
bob.print_age()

print(bob.name)
print(bob.age)

print(hasattr(bob, "age"))
print(hasattr(bob, "asd"))

print(getattr(bob, "age"))
setattr(bob, "asd", 100)

print(getattr(bob, "asd"))
delattr(bob, "asd")

# print(getattr(bob, "asd"))

print(Person.wants_to_hack)
print(bob.wants_to_hack)
print(alice.wants_to_hack)
print(mallory.wants_to_hack)

Person.wants_to_hack = "No way!"

print(Person.wants_to_hack)
print(bob.wants_to_hack)
print(alice.wants_to_hack)
print(mallory.wants_to_hack)

bob.wants_to_hack = "Yes!"

print(Person.wants_to_hack)
print(bob.wants_to_hack)
print(alice.wants_to_hack)
print(mallory.wants_to_hack)

bob.print_name()
del bob.name
#bob.print_name()

#del Person
print(alice.name)

print(Person.__dict__)
print(Person.__doc__)
print(Person.__name__)
print(Person.__module__)
```

## Inheritance

- a way of creating a new class by using details of an already existing class, but without needing to make any changes to that existing class
- the existing class is the **parent / base class**

```python
class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.age = age

	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.age))

	def birthday(self):
		self.age += 1

class Hacker(Person):
	def __init__(self, name, age, cves):
		super().__init__(name, age)
		self.cves = cves

	def print_name(self):
		print("My name is {} and I have {} CVEs".format(self.name, self.cves))

	def total_cves(self):
		return self.cves

bob = Person("bob", 30)
alice = Hacker("alice", 20, 5)

bob.print_name()
alice.print_name()

print(bob.age)
print(alice.age)

bob.birthday()
alice.birthday()

print(bob.age)
print(alice.age)

print(alice.total_cves())
#print(bob.total_cves())

print(issubclass(Hacker, Person))
print(issubclass(Person, Hacker))

print(isinstance(bob, Person))
print(isinstance(bob, Hacker))

print(isinstance(alice, Person))
print(isinstance(alice, Hacker))
```


## Encapsulation

- The idea of restricting access
- can prevent the accidental modification of data by creating private variables and methods

```python
class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.__age = age

	def get_age(self):
		return self.__age

	def set_age(self, age):
		self.__age = age

	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.__age))

	def birthday(self):
		self.__age += 1

bob = Person("age", 30)
#print(bob.__age)
print(bob.get_age())

bob.set_age(31)
print(bob.get_age())

bob.birthday()
print(bob.get_age())

print(bob.__dict__)

bob._Person__age = 50
print(bob.get_age())
```


## Polymorphism

- the ability in OOP to use a common interface for multiple different types
- ex: we can use the exact same function even if we pass in different types to that

```python
print(len("string"))
print(len(['l','i','s','t']))

class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.age = age

	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.age))

	def birthday(self):
		self.age += 1

class Hacker(Person):
	def __init__(self, name, age, cves):
		super().__init__(name, age)
		self.cves = cves

	def print_name(self):
		print("My name is {} and I have {} CVEs".format(self.name, self.cves))

	def total_cves(self):
		return self.cves

bob = Person("bob", 30)
alice = Hacker("alice", 25, 10)
people = [bob, alice]

for person in people:
	person.print_name()
	print(type(person))

def obj_dump(object):
	object.print_name()
	print(object.age)
	object.birthday()
	print(object.age)
	print(object.__class__)
	print(object.__class__.__name__)

obj_dump(bob)
obj_dump(alice)
```


## Operator Overloading


```python
print(1 + 1) # addition 
print("1" + "1") # concatenation

class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.age = age

	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.age))

	def birthday(self):
		self.age += 1

	def __str__(self):
		return "My name is {} and I am {} years old".format(self.name, self.age)

	def __add__(self, other):
		return self.age + other.age

	def __lt__(self, other):
		return self.age < other.age

bob = Person("bob", 30)
alice = Person("alice", 35)

print(bob)
print(bob + alice)
print(alice + bob)

print(bob < alice)
print(alice < bob)
```



## Class Decorators

- combining decorators and classes enables you as the programmer to create and control more complex classes and object instances by centralizing and reusing code and structures

```python
class Person:
	'Person base class'
	wants_to_hack = True # class attribute

	def __init__(self, name, age):
		self.name = name
		self.__age = age

	def get_age(self):
		return self.__age

	def set_age(self, age):
		self.__age = age

	@property
	def age(self):
		return self.__age
	
	@age.setter
	def age(self, age):
		self.__age = age 

	@age.deleter
	def age(self):
		del self.__age

	@classmethod
	def wants_to(cls):
		return cls.wants_to_hack

	@classmethod
	def bob_factory(cls):
		return cls("bob", 30)

	@staticmethod
	def static_print():
		print("I am the same!")


	def print_name(self):
		print("My name is {}".format(self.name))

	def print_age(self):
		print("My age is {}".format(self.__age))

	def birthday(self):
		self.__age += 1

bob = Person("bob", 30)
print(bob.age)

bob.age = 50
print(bob.age)

#del bob.age
#print(bob.age)

print(Person.wants_to())

bob1 = Person.bob_factory()
bob2 = Person.bob_factory()
bob3 = Person.bob_factory()

bob1.print_name()
bob2.print_name()
bob3.print_name()

Person.static_print()
bob1.static_print()
bob2.static_print()
bob3.static_print()
```

