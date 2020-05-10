Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example,6, 8 are ugly while 14 is not ugly since it includes another prime factor7.

Note that 1 is typically treated as an ugly number.
#

```python
class Solution:
    def isUgly(self, num: int) -> bool:
        if num == 1: return True
        while num != 0 and (num % 2 ==0 or num % 3 == 0 or num % 5 == 0):
            if num % 2 == 0: num //= 2
            elif num % 3 == 0: num //= 3
            elif num % 5 == 0: num //= 5
        return num == 1
            
```