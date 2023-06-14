
## Welcome and course introduction

![[Pasted image 20230504140516.png]]
![[Pasted image 20230504140701.png]]

![[Pasted image 20230504140955.png]]


## Decorators

- allow you to modify the behaviour of a function without modifying the function
- to create a decorator function, we need am outer function that takes a function as an argument
- we also need an inner function that wraps around the decorated function

```Python
from datetime import datetime
import time

def logger(func):
    def wrapper():
        print("-"*50)
        print("> Execution started {}".format(datetime.today().strftime("%Y-%m-%d %H:%M:%S")))
        func()
        print("> Execution completed {}".format(datetime.today().strftime("%Y-%m-%d %H:%M:%S")))
        print("-"*50)
    return wrapper 
        
@logger
def demo_function():
    print("Executing task!")
    time.sleep(3)
    print("Task completed!")

#demo_function()

#logger(demo_function())

def logger_args(func):
    def wrapper(*args, **kwargs):
        print("-"*50)
        print("> Execution started {}".format(datetime.today().strftime("%Y-%m-%d %H:%M:%S")))
        func(*args, **kwargs)
        print("> Execution completed {}".format(datetime.today().strftime("%Y-%m-%d %H:%M:%S")))
        print("-"*50)
    return wrapper

@logger_args
def demo_function_args(sleep_time):
	print("Executing task!")
	time.sleep(sleep_time)
	print("Task complete!")

demo_function_args(1)
demo_function_args(5)
```


## Generators

- provide a simple way to create iterators generators,  return iterable set of items one at a time
```Python
def gen_demo():
	n = 1
	yield n

	n += 1
	yield n

	n += 1
	yield n

test = gen_demo()
print(test)

print(next(test))
print(next(test))
print(next(test))

test2 = gen_demo()
for a in test2:
	print(a)

def xor_static_key(a):
	key = 0x5
	for i in a:
		yield chr(ord(i) ^ key)

for i in xor_static_key("test"):
	print(i)

xor_static_key2 = (chr(ord(i) ^ 0x5) for i in "test")

print(xor_static_key2)
print(next(xor_static_key2))
print(next(xor_static_key2))

for i in xor_static_key2:
	print(i)
```


## Serialization

- the process of translating data structures or objects into a format that can be stored or transmitted, and then later reconstructed by deserializing the serilazed object.

```python
import pickle

hackers = {"neut": 1, "geohot": 100, "neo": 1000}

for key, value in hackers.items():
	print(key, value)

serialized = pickle.dumps(hackers)
print(serialized)

hackers_v2 = pickle.loads(serialized)
print(hackers_v2)

for key, value in hackers_v2.items():
	print(key, value)

# with open("hackers.pickle", "wb") as handle:
# 	pickle.dump(hackers, handle)

with open("hackers.pickle", "rb") as handle:
	hackers_v3 = pickle.load(handle)

print(hackers_v3)
```


## Closures

**Nested function** = a file inside another function
- has access to variables in the enclosing scope

```python
def print_out(a):
    print("Outer: {}".format(a))

    def print_in():
        return "\tInner: {}".format(a)

    return print_in

test2 = print_out("test")
del print_out
print(test2())
```
