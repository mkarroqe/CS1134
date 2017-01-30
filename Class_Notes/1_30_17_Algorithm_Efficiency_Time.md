# Algorithm Efficiency: Time
* Topic *
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
1. Version 1:
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
   ```
  
