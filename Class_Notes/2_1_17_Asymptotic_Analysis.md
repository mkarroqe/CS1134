## Asymptotic Analysis
#### Example
Show that 3n^2 + 6n - 15 = bigtheta(n^2)
##### Proof:
Take c1 = _______
     c2 = _______
     n0 = _______
    
Where do we start? by sketching some shit ok here we go

3n^2 = 3n^2 + 0 <= **3n^2 + 6n - 15** <= 3n^2 + 6n <= 3n^2 + 6n^2 = 9n^2 (we make it bigger by subtracting 15, but it's still not ??)

ok so now we can make c1 = 9 and c2 = 3 for some reason, i will consult the textbook and report back
n0 = 3

ok so here's the proof:
for all n >= 3 we have:
I) **3n^2 + 6n - 15** <= 3n^2 + 6n <= 3n^2 + 6n^2 = 9n^2
II) Since n >= 3 ==> 6n >= 18 >= 15 ==> 6n >= 15 ==> 6n-15 >= 0
    Therefore for n >= 3 we have:
    3n^2 + 6n - 15 >= 3n^2 + 0 = 3n^2
                   ^6n-15 >=0
III) All together we get that for n >= 3:
     3n^2 <= 3n^2 + 6n - 15 <= 9n^2
                   
("I'm supposed to look for two multiplicand of g that bind f from below and above")
===
#### Example
Let's figure out the running time of this function as a function of n (T1(n)):

```python
def print_square(n):
     for i in range(n):
          line = '*' * n
          print(line)
```
First, *what does it do?* It prints a square of `*` of length and width `n`.
Second, *what's the running time of the entire loop execution?* Let's start from the inside and out.
     First, the cost of what's inside the for loop
          
          ```python
               line = '*' * n
               print(line)
          ```
     The first line here won't be a primitive operation; no matter what the input is, it'll take the same about of time
     This line is *linear* of `n`, so it would cost **theta(n)**
          
     Then, we move on to the for loop, which is theta(n^2)
     So it's theta(n^2).  Wack.  I will consult the textbook later
     
#### Example
```python
def print_triangle(n):
     for i in range(1, n + 1):
          line = '*' * i
          print(line)
```
**_What's the asymptotic order of the above function?_**    

We need to figure out the cost of the for loop, but in order to do that we need to find out how much we pay for each body and then sum it for all the different iterations.

You'll see that here, the body varies from iteration to iteraiton.  In this case, it kind of matters the value of i.  the cost of the line line costs theta(i).  It's O(n), it's not more than n (?) so the inner chunk inside the for loop is theta(i).

     And actually it makes sense because i is a variable that has influence over this body so the excecution the cost the runtime of this body can be dependent on i

Ok, so now let's figure out the cost of the for loop.  When you find the cost of a for loop, think of it as a *summation*, not as a multiplicaiton.  A lot of times we want to add stuff we're executing.  We need to add the accurate about of each iteration.

In this case, we would need to add 1 + 2 + 3 + ... + n.  Only the last one would actually cost us n.
We have some formula (n(n+1))/2 = (1/2)n^2+(1/2)n = theta(n^2)

You can prove it by definition.  Neat.  Again, I will be consulting the textbook to fix and explain.  Much love to all 0 people following this repo <33

**Look at diagram!! The triangle is half the number of stars as the square function is (nice visual!!!!!)**

===

#### Example

```python
# search function that will return the index of the value `val` inside `lst`.  If it does not exist, we return `None`.
def linear_search(lst, val):
     for i in range(len(lst):
          if lst[i] == val:
               return i
     return None
```

Now we analyze the run time of this function as a function of the input size.  In the case of a list, the input size is obviously the length of the list.  In this case, T(n), n is the length of lst. 

Now, how long it will take this to excecute totally depends on what you pick; it could take one iteration but it could also take iterating through the entire list.  So, we take the worst case scenario.

* We compare the asymptotic order of the number of primitive operations excecuted by a process as a function of its input size in its worst case run.

So now we do this evaluation:
The function has two parts: the for loop and the return.  The return is worth theta(1) so the for loop is dominant.  The for loop is a constant execution of the body (remember its a summation).  The if statement is theta(1) and the for loop is theta(n).

That is why it is called a linear function, because yeah. textbook

===

Here, we are searching a sorted list.  How can we make this a better algorithm?  Again, think of the worst case.  Binary search is a good alternatibe algorithm!  Will it make a difference asymptotic wise, though?

```python
# this time, we are searching a sorted list.
def binary_search(srt_list, val):
     left = 0
     right = len(srt_lst) - 1
     found = False
     
     while(found == False):
          mid = (left + right) // 2 # floored average
          if srt_list[mid] == val):
               found = True
               ind = mid
          elif val < srt_lst[mid]:
               right = mid - 1
          else: # val > srt_lst[mid]:
               left = mid + 1
               
     return ind
     
     
     
     
     
     
     
     
     
     
     

          
