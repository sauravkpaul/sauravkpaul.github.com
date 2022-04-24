---
layout: post
title:  Backtracking, DFS problems approach in C++, Java
categories: [Backtracking,DFS,Recursion]
---

Below are some similar ***Leetcode*** questions which can be solved via ***backtracking***.
This is a general template for all permutations, combination and subset related problems

## [78. Subsets](https://leetcode.com/problems/subsets/)

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:

Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

#### Backtracking Solution

##### C++

```c++
class Solution {
private:
    void backtrack(vector<vector<int>>& list , vector<int>& tempList, vector<int>& nums, int start) {
        list.push_back(tempList);

        for(int i = start; i < nums.size(); i++) {
                tempList.push_back(nums[i]);
                backtrack(list, tempList, nums, i + 1);
                tempList.pop_back();
        }
    }
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> list;
        sort(nums.begin(), nums.end());
        vector<int> out;
        backtrack(list, out, nums, 0);
        return list;
    }
};
```
##### Java

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list , List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```

## [90. Subsets II](https://leetcode.com/problems/subsets-ii/)
Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.



Example 1:

Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

##### C++

```c++
class Solution {
private:
    void
    backtrack(vector<vector<int>>& list , vector<int>& tempList, vector<int>& nums, int start) {
        list.push_back(tempList);

        for(int i = start; i < nums.size(); i++) {
            if(i > start && nums[i] == nums[i-1]) continue; //Skip Duplicates
            tempList.push_back(nums[i]);
            backtrack(list, tempList, nums, i + 1);
            tempList.pop_back();
        }
    }

public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> list;
        sort(nums.begin(), nums.end());
        vector<int> out;
        backtrack(list, out, nums, 0);
        return list;
    }
};
```

#### Java

```java
public List<List<Integer>> subsetsWithDup(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        if(i > start && nums[i] == nums[i-1]) continue; // skip duplicates
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```

## [46. Permutations](https://leetcode.com/problems/permutations/)
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

##### C++

```c++
class Solution {
public:
    void backtrack(vector<int>& n, vector<int> &out, vector<vector<int>> &res) {
        if(out.size() == n.size()) {
            res.push_back(out);
        } else {
            for(int i =0; i < n.size() ; i++) {
                if (std::find(out.begin(), out.end(), n[i])  != out.end()) { continue; }
                out.push_back(n[i]);
                backtrack(n, out, res);
                out.pop_back();
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> out;
        backtrack(nums, out, res);
        return res;
    }
};
```

##### Java

```java
public List<List<Integer>> permute(int[] nums) {
   List<List<Integer>> list = new ArrayList<>();
   // Arrays.sort(nums); // not necessary
   backtrack(list, new ArrayList<>(), nums);
   return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums){
   if(tempList.size() == nums.length){
      list.add(new ArrayList<>(tempList));
   } else{
      for(int i = 0; i < nums.length; i++){
         if(tempList.contains(nums[i])) continue; // element already exists, skip
         tempList.add(nums[i]);
         backtrack(list, tempList, nums);
         tempList.remove(tempList.size() - 1);
      }
   }
}
```


## [47. Permutations II](https://leetcode.com/problems/permutations-ii/)
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

#### C++

```c++
class Solution {
public:
    void backtrack(vector<int>& n, vector<int> &out,
                    vector<vector<int>> &res, vector<bool> &used) {
        if(out.size() == n.size()) {
            res.push_back(out);
        } else {
            for(int i =0; i < n.size() ; i++) {
                if(used[i] || (i > 0 && n[i] == n[i-1] && !used[i - 1])) {continue;}
                out.push_back(n[i]);
                used[i] = true;
                backtrack(n, out, res, used);
                out.pop_back();
                used[i] = false;
            }
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        vector<int> out;
        vector<bool> used(nums.size(), false);
        sort(nums.begin(), nums.end());
        backtrack(nums, out, res, used);
        return res;
    }
};
```

#### Java

```java
public List<List<Integer>> permuteUnique(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, new boolean[nums.length]);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, boolean [] used){
    if(tempList.size() == nums.length){
        list.add(new ArrayList<>(tempList));
    } else{
        for(int i = 0; i < nums.length; i++){
            if(used[i] || i > 0 && nums[i] == nums[i-1] && !used[i - 1]) continue;
            used[i] = true;
            tempList.add(nums[i]);
            backtrack(list, tempList, nums, used);
            used[i] = false;
            tempList.remove(tempList.size() - 1);
        }
    }
}
```

## [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is guaranteed that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

Example 1:
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.


#### C++

```c++
class Solution {
public:
    void backtrack(vector<int>& c, int t, int pos, vector<int>& out, vector<vector<int>>& res) {
        if(t < 0){ return; }
        else if (t == 0) { res.push_back(out); }
        else {
            for (int i = pos; i < c.size(); i++) {
                out.push_back(c[i]);
                backtrack(c, t-c[i], i, out, res); //not i+1 because we can reuse some of the elements.
                out.pop_back();  
            }
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> res;
        vector<int> out;
        backtrack(candidates, target, 0 , out, res);
        return res;
    }
};
```

#### Java

```java
public List<List<Integer>> combinationSum(int[] nums, int target) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, target, 0);
    return list;
}

private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, int remain, int start){
    if(remain < 0) return;
    else if(remain == 0) list.add(new ArrayList<>(tempList));
    else{
        for(int i = start; i < nums.length; i++){
            tempList.add(nums[i]);
            backtrack(list, tempList, nums, remain - nums[i], i); // not i + 1 because we can reuse same elements
            tempList.remove(tempList.size() - 1);
        }
    }
}
```
