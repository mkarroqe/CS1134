# Classes, Iterators, and List Comprehension 
*Introducing `yield`, `iter()`, and `next()`.*
#### Lecture Date: 1.23.17
---
## Review of Classes
#### Example:
```python
class Counter:
    def __init__(self, init_val = 0):
        self.val = init_val # constructor
    def print_and_inc(self):
        print(self.val)
        self.val += 1

c1 = Counter() # creating a Counter object
c1.print_and_inc() # 0
c2 = Counter()
c2.print_and_inc() # own thing, see diagram
```
The above code instantiates a new class `Counter`.  The `__init__(self, init_val = 0)` function is the constructor; it creates the `Counter` object, setting the default value to 0.  The `print_and_inc(self)` function increments the object by 1.

## List Comprehension
First, we created 2 Counter objects (see above class).
```python
lst1 = [Counter()] * 5 # list of 5 Counter objects ? no see below
lst2 = [Counter() for i in range(5)] # list of 5 Counter objects
```
When we loop through them and increment them, we get the following outputs:

| code | output |
| --- | --- |
| `for c in lst1:` <br> &nbsp;&nbsp;&nbsp;&nbsp; `c.print_and_inc()` | `0 1 2 3 4` |
| `for c in lst2:` <br> &nbsp;&nbsp;&nbsp;&nbsp; `c.print_and_inc()` | `0 0 0 0 0` |

### <u> Explanation: </u> <!-- I know its deprecated fight me about it -->
#### `lst1`:
(See picture 2)
lst1 is a list of length 5;
we are creating one object, and all elements are pointing to that same object
therefore, when we call print_and_inc, they are all changing the same counter

#### `lst2`:
(See picture 2)
in lst2, we are creating 5 different counter objects
therefore, when we call print_and_inc, we are affecting different objects each time, getting 0

# ----------------------------

def square_lst(lst):
    res = []
    for elem in lst:
        res.append(elem * elem)
    return res

def inc_lst(lst):
    res = []
    for elem in lst:
        res.append(elem + 1)
    return res

# how can we generalize the above 2 functions into one?  They both have the same algorithmic template.
# by passing a function as a parameter! (Is a function considered a datatype then?) no, but they are objects with their own type

def map_list(lst, func): # High Order Function: a function that takes another function as an argument
    res = []
    for elem in lst:
        res.append(func(elem))
    return res
# ha! cool

# so now, we can call square_lst() as:
def square(x):
    return x * x

def square_lst(lst):
    return map_lst(lst, square)

# and we can call inc_lst as:
def inc(x):
    return x + 1

def inc_lst(lst):
    return map_list(lst, inc)

# that's it! d o p e
# consider the appications with a long af algorithm
# "functions are also a form in which we can generalize our ideas."

# ----------------------------

# something something for loops
for var in iterable:
  # examples of iterable collections: lst, str, dict, range, etc
  # iterable object: an object that produces an iterator by calling the iter() function
  # calls next(), assigns it to var, excecutes the body and repeat

# Example:
lst = [1, 2, 3]
lst_iterator = iter(lst)
s = 'abc'
s_iterator = iter(s)
r = range(4)
r_iterator = iter(r)

# so wtf is an iterator?
# iterator object: an object that iterates over a series of values by making subsequent calls to the next() function.
# After ending the sequence, a call to next() would raise a StopIteration exception

# well wtf is the next() function?
next(lst_iterator)
# self explanatory; gets the next element in a function

for item in range(4):
    print(item)

# ok, now let's make a diy for loop to appreciate what it does for us
r = range(4)
r_iterator = iter(r)
end = False

while(end == False):
    try:
        item = next(r_iterator)
        print(item)
    except StopIteration:
        end = True

# ----------------------------

# built in iterable objects:
    # range()
        # this is different that list/string
        # has to take in data
        # list and string are objects that store them constantly inside memory;
        # this is not the case with range!
            # a range(4) does not store 4 integers stored in memory, unlike a list or string.
                # think of application in a range of 1000000!
            # range is more effective in storage
            # it's an implicit series of values; they are created as we proceed
    # list, string

# example of how range does its thang
def f():
    x = 1
    yield x # sort of like return but not really

    x += 1
    yield x

    x += 1
    yield x

    # f is a function
# but, if we do this:
temp = f()
    # here, temp's type is something new: a generator

# wtf is a generator?
# generator: another type of iterable object

# that means we can create an iterator out of it:
temp_iterator = iter(temp)
next(temp) # would give 1, 2, 3 each time its run (test in console!)

# yield acts like a pause button.  cool! diy range function

# lets officially define our own range function:
def my_range_lst(start, stop, step = 1):
    res = []
    curr = start
    while(curr < stop):
        res.append(curr)
        curr += step
    return res # this is a list
# later on, we can do something like:
for i in my_range_lst(1, 10, 0.5):
    print(i) # creates a list of all the values; they are all stores in memory at the same time
             # run in console to demonstrate

# how can we do this using generators? without storing them inside the memory all at once?
def my_range(start, stop, step = 1):
    curr = start
    while(curr < stop):
        yield curr # using yield ofc
        curr += step

for i in my_range_lst(1, 10, 0.5):
        print(i)

# using a generator object is considered "lazy"; the regular was creates all the elements upfront, even if you don't need all of them.  generator makes them on-demand

# ----------------------------

# example where we're finding all factors of a number
def factors(num):
    # generate factors on demand using the yield to be more efficient in space
    for curr in range(1, num + 1):
        if num % curr == 0:
            yield curr

for item in factors(100):
    print(item)
