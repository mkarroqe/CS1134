# Algorithm Efficiency: Time
*Topic*
#### Lecture Date: 1.30.17
---
## Primality Testing
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
