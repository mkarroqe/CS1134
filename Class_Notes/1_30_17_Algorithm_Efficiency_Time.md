# Algorithm Efficiency: Time
*Topic*
#### Lecture Date: 1.30.17
---
## Primality Testing
Testing if numbers are prime.

### Definitions:
1. Let `num>=2` be an integer.  We say that `num` is prime if its only divisors are 1 and `num`.
  * 13 is prime
  * 12 is not
2. Let `num>=2` be an integer, and let `d` and `k` be two divisors of `num`.  We say thatWe say that `k` and `d` are complementary divisors of `num` if `d * k = num`.
  * 4 and 25 are complementary divisors of 100
  * so are 5 and 20
  
### Implementation:
1. Version 1: iterating over the entire range to look for all divisors and track them in a counter.  If there are only 2, it is prime by definition.  If there are more, then it is not.
  * ```python
  def is_prime1(num):
      count_divs = 0
      
      for curr in range(1, num + 1):
          if(num % curr == 0):
              count_divs += 1
      
      if(count_divs == 2):
          return True # if we have two divisors, it's prime
      else:
          return False
      ``````
2. Version 2: iterating over first half of the range to be more efficient; 
  
  * Proof: showing that there are no divisors in the second half to show `num` is prime
   (TODO: fix sloppy proof)

   Let `k` be a divisor of `num` in the second half of the range.  That is, `k > num/2`.
   Let `d` be `k`'s complementary divisor, therefore `d = num/k`.

   Let's compare:
   `d = num/k` **<** `num/(num/2)` = `num/1 * 2/num = 2`

   Therefore `d < 2` Which means that it only can be equal to 1.

  * Code:
  ```python
  def is_prime2(num):
      count_divs = 0
      
      for curr in range(1, num // 2 + 1): # range cannot accept floats
          if(num % curr == 0):
              count_divs += 1
      
      if(count_divs == 1): # since we're onlt going over the first half of the range, we only need to find one divisor for it to be prime.
          return True
      else:
          return False
  ```
3. Version 3: 1, 2, 3, ..., sqrt(num), ... num
  * Proof by contradiction:
  Let's assume that both complementary divisors, `k` and `d`, are both after sqrt(num) in the second part.
  
  num = k 8 d > sqrt(num) * sqrt(num) = num
  Which implies that num > num with is fALsE aF
  
  * Code:
  ```python
  import math
  
  def is_prime3(num):
      count_divs = 0
      
      for curr in range(1, int(math.sqrt(num)) + 1):
          if(num % curr == 0):
              count_divs += 1
      
      if(count_divs == 1): # we only need to find one divisor for it to be prime. TODO: explain why
          return True
      else:
          return False
  ```
### Regarding Efficiency in Runtime:
It seems like `is_prime3` > `is_prime2` > `is_prime1`, denoted by the constants `T3`, `T2`, and `T1`, respectively.
But the professor is implying that he's about to disprove that soon.

## Testing Runtime
On a standard measure for running time of algorithms:
* Observations:
  1. The running time depends on the input.
    * Runtime values are not constant values; their values depend on the `num` passed into the function.
    * We parameterize the running time by the size of the input.
      * `T1(n)`, `T2(n)`, `T3(n)`
  2. The running time depends on the operations we use and the type we apply them on.
    * `int`s are faster than `float`s
    * We count all primitive operations as 1.
      * addition, subtraction, etc
      * assignment of variables, etc
    * Informal running time criteria:
      * We compare the number of primitive operations the algorithms excecute as a function of the input size.
      * We compare the *order of growth* of primitive operations ...
        * order of growth:
          * `T(n) = 3n^2 + 6n - 15 = bigtheta(n^2)
            * you can ignore second part of equation (lower order terms: 6n-15) and the constant (3)
            * so w this, 
              * `T1 = bigtheta(n)`
              * `T2 = bigtheta(n)` o shit
              * `T3 = bigtheta(sqrt(n))` so this algorithm is superior
        * asymptotic growth is how we evaluate our algorithms now
      
      * Testing:
        1. `is_prime1(num)`
          1. variable assignment
          calling next
          assigning to curr
          (TODO: properly count these)

          `T1(n) = 1 + 1 + (5 * n) + 2 = 5n + 4`

        2. `is_prime2(num)`
          1. initializing var
          2. for loop 
           1 for initial iter
            calling next
            assigning curr
            ... somehow he counted 5

          `T2(n) = 1 + 1 + (5 * n/2) + 2 = 2.5n + 4`

        3. `is_prime3(num)`
          1. init var
          2. two at the end
          3. in loop: same 5 operations sqrt(n) times

          `T3(n) = 1 + 1 + 5sqrt(n) + 4`

      So which one is most efficient now? It depends on the input.  For values 1, 2, 3, `T2` is best, but after, `T3` is best.
      
  3. The running time depends on the hardware environment.
    * We make asymptotic analysis looking at the order of growth.
    * Big O
      * 
    * Big Theta















