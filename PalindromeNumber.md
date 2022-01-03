# Palindrome Number

Given an integer x, return true if x is palindrome integer.

An integer is a palindrome when it reads the same backward as forward.

For example, 121 is a palindrome while 123 is not.

__Example 1:__

```
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```
### First Attempt - description
----
```python
def isPalindrome(x) -> bool:
        n = x
        if (x<0):
            return False
        # find digits
        # number of digits
        digits = 0
        while n >= 1:
            n /= 10
            digits += 1
        
        n = x
        while digits>1:
            d = (n - (n % (10**(digits-1))))/10**(digits-1) # get first digit of the number
            print(d)            
            l = n % 10 # get last digit
            print(l)
            if (d != l):
                 return False
                 
            # remove first digit of number
            n -= d*(10**(digits-1))
            print(n)
            # remove last digit
            n -= l
            n/=10
                 
            digits -= 2
        return True
```

- method
    - time complexity - I have no idea
    - space complexity - created extra copy of n

### Revert half the number
----
```python
def isPalindrome(x) -> bool:
    if ((x < 0) or (x % 10 == 0 and x != 0)): # special cases
        return False

    revertedNumber = 0
    while(x > revertedNumber):
        revertedNumber = revertedNumber * 10 + x%10
        x = int(x/10)
    
    return (x==revertedNumber) or (x==int(revertedNumber/10))
```
- Faster because of less copying and only one comparison
- also didn't know you can manipulate x 
