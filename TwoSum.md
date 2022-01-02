# Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

__Example 1:__

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```
### First Attempt - Brute Force
----
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for y in range(1, len(nums)):
                if(nums[i]+nums[y] == target and (i != y)):
                    
                    return [i,y]
```

- Brute force 
    - O(n<sup>2</sup>) time complexity - nested for loops
    - O(1) space complexity

### 2-pass Hash Table
----
A hash table is well suited for this purpose because it supports fast lookup in near constant time. I say "near" because if a collision occurred, a lookup could degenerate to O(n) time. However, lookup in a hash table should be amortized O(1) time as long as the hash function was chosen carefully.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)): # first pass
            hashmap[nums[i]] = i # number:index
        for i in range(len(nums)): # second pass
            complement = target - nums[i] # number to search for
            if complement in hashmap and hashmap[complement] != i:
                return [i, hashmap[complement]] 
```
- This works because you don't have to iterate through to find the complement. `in` is faster because of ```dict```
- Each call of `in` is O(1) and so traversing through the list gives:
    - O(n) time complexity
    
    - O(n) space complexity 
        - create a dict of length n


### 1-pass Hash Table
----
It turns out we can do it in one-pass. While we are iterating and inserting elements into the hash table, we also look back to check if current element's complement already exists in the hash table. If it exists, we have found a solution and return the indices immediately.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i, num in enumerate(nums)):
            complement = target - num
            if complement in hashmap: # early exit
                return [i, hashmap[complement]]
            hashmap[nums[i]] = i # otherwise keep making the hashmap
```
- Same idea as above, only there is a shortcut by checking the unfinished hashmap to exit early
- Same time and space complexity, but simpler.