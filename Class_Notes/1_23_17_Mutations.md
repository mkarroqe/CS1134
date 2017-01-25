# Python Review: Mutations 
#### Lecture Date: 1.23.17
---
[variable_map]: images/1_23_17_img1.png "Variable Map"
[lists_map1]: images/1_23_17_img2.png "Lists Map"

## Declaring Variables:
When you declare a variable, for example, ```x = 4```, an int object is created of value 4.  The variable ```x``` then points to that int object.
If you reassign the value of ```x``` to ```x = 3.5```, a float, a new float object is created and the variable ```x``` will then point to that instead.

![alt text][variable_map]

# Lists / Mutating Lists: MUTABLE DATA STRUCTURES   
```python
lst = [1, 2, 3]
for elem in lst:
     elem += 10
 ```
The above list lst will not be mutated because elem is a copy of the actual element in the list.  Lists are mutable, but here, only the copy is being mutated.  New values are being changed.

To mutate the element in the list, you must use the indicies:
    
```python
for idx in range(3):
   lst[idx] = lst[idx] + 10
```

##### Example:
First, we're creating three lists, `lst1`, `lst2`, and `lst3`, respectively.
```python
lst1 = [1, 2, 3] # lst1 is pointing to its own new object
lst2 = lst1 # lst2 is pointing to the same object as lst1; same memory address
lst3 = [1, 2, 3] # lst3 is pointing to its own new object
```
You can see in the diagram below how they are stored and referenced in memory:

![alt text][lists_map1]

Then, we append to the lists to demonstrate how they are affected in memory.
```python
lst1.append(4) # lst2 is also affected when this happens
lst2.append(5) # lst1 is also affected when this happens
lst3.append(6) # is independent
```
Printing the lists outputs the following:

Code | Output
--- | ---
`print("lst1:", lst1)` | `lst1: [1, 2, 3, 4, 5]`
`print("lst2:", lst2)` | `lst2: [1, 2, 3, 4, 5]`
`print("lst3:", lst3)` | `lst3: [1, 2, 3, 6]`


# Strings / Mutating Strings: IMMUTABLE DATA STRUCTURES
    s1 = "abc" # points to new string object
    s2 = s1 # points to the same memory address/string object as s1
    s1 = s1 + "d" # UNLIKE LISTS, STRINGS ARE IMMUTABLE.  This is creating a new string instance that contains the data "abcd".  Now, s1 and s2 no longer point to the same memory address.
    s2.upper() # creates new string "ABC" but it is not being assigned to anything; is not pointed anywhere.
    '''
    print("s1:", s1)
    print("s2:", s2)
    '''
    # Example 1
    lst1 = [1, 2, 3]
    lst2 = lst1.copy() # Since it is a copy, a new list object is created.  HOWEVER, the data (elements) in the copy point to the original list it copied.
    lst1[0] = 10 # This creates a new reference for the first element, 10, but the 1 does not disappear, and the value of the copy does not change.
    '''
    print("lst1:", lst1)
    print("lst2:", lst2)
    '''
    # Example 2
    lst1 = [[1, 2], 3, [4, 5]]
    lst2 = lst1.copy() # even though this is a copy, BOTH lists are mutated. (See diagram)  The value the copy is pointing to is also mutated.
    lst1[0][0] = 10
    '''
    print("lst1:", lst1)
    print("lst2:", lst2)
    '''

    # Clearly, we have a problem with the copy() function (shallow copy) when we use it on more complex data structures.
    # To make a deep copy:
    import copy
    lst1 = [[1, 2], 3, [4, 5]]
    shallow_lst1 = copy.copy(lst1)
    deep_lst1 = copy.deepcopy(lst1)

    shallow_lst1[0][0] = 10
    deep_lst1[0][1] = 20
    '''
    print(shallow_lst1)
    print(deep_lst1)
    '''
    # More reading: https://docs.python.org/2/library/copy.html

# Mutating Lists and Copies Cont.

def main():
    main_lst1 = [1, 2, 3]
    fun1(main_lst1)
    print("main list1", main_lst1)

    main_lst2 = [1, 2, 3]
    fun2(main_lst2)
    print("main list2", main_lst2)

def fun1(lst):
    for ind in range(len(lst)):
        lst[ind] += 10
    print("lst =", lst)

    # both lst1 and main_lst1 are mutated to the same thing, because the same object is mutated.

def fun2(lst):
    lst.append(4)
    lst = [1, 2, 3]
    lst.reverse()
    print("lst =", lst)

    # lst2 is mutated, but once lst is assigned to a new memory address, a new lst object, it stops being mutated

# see diagrams

# LIST COMPREHENSION SYNTAX
# [<expression> for <var> in <iterable-collection>]
res = []
for k in range(1, 11):
    res.append(k * k)
'''print("res:", res)'''

# alt syntax of same thing:
res = []
squares = [k * k for k in range(1, 11)] # creates a list in one line whoop
                                        # similar to math notation {10k + 3} 1 <= k <= 5
                                        #                      vs. {13, 23, 33, 43, 53} lit

# w strings: creating a list of ascii values in a letter
str = "text"
ascii_of_str = [ord(letter) for letter in str] # dope

# [<expression> for <var> in <iterable-collection> if <condition>]
odds = [k for k in range(1, 11) if (k % 2) == 1]

factors = [k for k in range(1, 101) if (100 % k == 0)]
