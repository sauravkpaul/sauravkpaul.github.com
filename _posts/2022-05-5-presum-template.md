---
layout: post
title:  Presum pattern for Subarray Sum Problems
categories: [presum, arrays]
---

Below are some similar ***Leetcode*** questions which can be solved via ***presum*** pattern.
In this pattern we calculate a presum of each element in array to calculate possible sum targets.

Count sum while looping through every element in array . store every pre_ssum:count , if any pre_s[sum] >0, add into result.

```
unordered_map<int, int> c({{0, 1}});
int psum = 0, res = 0;
for (int i : A) {
    psum += i;
    res += c[psum - S];
    c[psum]++;
}
return res;
```

## [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/submissions/)
Given an array of integers nums and an integer k, return the total number of subarrays whose sum equals to k.
A subarray is a contiguous non-empty sequence of elements within an array.
### Solution
Here as well we use the presum template to solve

```c++
class Solution {
public:
    int subarraySum(vector<int>& A, int S) {
        unordered_map<int, int> c({{0, 1}});
        int psum = 0, res = 0;
        for (int i : A) {
            psum += i;
            res += c[psum - S];
            c[psum]++;
        }
        return res;
    }
}
```

## [930. Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/)

### Solution

```c++
class Solution {
public:
    int numSubarraysWithSum(vector<int>& A, int S) {
        unordered_map<int, int> c({{0, 1}});
        int psum = 0, res = 0;
        for (int i : A) {
            psum += i;
            res += c[psum - S];
            c[psum]++;
        }
        return res;
    }
};
```

## [523. Continuous Subarray Sum](https://leetcode.com/problems/continuous-subarray-sum/)
Given an integer array nums and an integer k, return true if nums has a continuous subarray of size at least two whose elements sum up to a multiple of k, or false otherwise.

An integer x is a multiple of k if there exists an integer n such that x = n * k. 0 is always a multiple of k.

The basic idea here is to look at the remainder of the sum, if it is repeating or not.
And if it is repeating, is it because of one element being divisible by k (which is not what we want i.e "false" case) or two elements being divisible by k
ex: [1,9,2,3] mod 9
sum % k will give us [1,1,3,6]
If we insert mod "immediately" in the same loop, this case will return a true

How is this being solved, by inserting pre "after" the look up is done

One interesting case is, what if the actual sum is divisible by k
ex: [1,2,3,4,5,7] mod 10
sum % k will give us [1,3,6,0,15,2] => valid subArray is [1,2,3,4]

The above algorithm solves this by pushing "0" in the very first loop. This way, if we encounter "0" anywhere else, we return true;

Also, k==0 is not required
mod = sum % k; // should be fine

same idea, different implementation

```c++
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        unordered_map<int,int> m; // store mod and position
        int sum=0, mod=0;
        /* This is needed to check if repeating mod is due to single element or not
           If prevDiv is false (which means prev element is not div), mod repeat is due to single element
           in which case, we need to check if there are more than one elements to return true
        */
        bool prevDiv=false;
        m[0]=-1;
        for(int i=0; i<nums.size(); i++){
            sum+=nums[i];
            mod=sum%k;
            if(m.find(mod)!=m.end()){
               if(prevDiv) return true;
               if(i-m[mod]>1)
                   return true;
            }
            else{
               m[mod]=i;
            }
            prevDiv = nums[i]%k == 0;
        }
        return false;
    }
}
```

## [974. Subarray Sums Divisible by K](https://leetcode.com/problems/subarray-sums-divisible-by-k/)
Given an integer array nums and an integer k, return the number of non-empty subarrays that have a sum divisible by k.

Example 1:

Input: nums = [4,5,0,-2,-3,1], k = 5
Output: 7
Explanation: There are 7 subarrays with a sum divisible by k = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]

### Solution

In this case since we have negatives as well. the formula (elem % k) + k takes care of negatives.


```c++
class Solution {
public:
    int subarraysDivByK(vector<int>& A, int K) {
        vector<int> count(K);
        count[0] = 1;
        int prefix = 0, res = 0;
        for (int a : A) {
            prefix = (prefix + a % K + K) % K;
            // or we can use prefix = Math.floorMod(prefix + a, K);
            res += count[prefix]++;
        }
        return res;
    }
};
```
