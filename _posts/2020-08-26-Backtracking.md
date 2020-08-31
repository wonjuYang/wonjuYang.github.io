---
title: "Backtracking"
categories: leetcode Backtracking
last_modified_at: 2020-08-26
---


# Backtracking



## Combination Sum


>[문제](https://leetcode.com/problems/combination-sum/)



### 내 답안


```javascript

/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
  var res = [];
  var len = candidates.length;
  candidates.sort((a, b) => (a - b));
  dfs(res, [], 0, len, candidates, target);
  return res;
};

var dfs = function (res, stack, index, len, candidates, target) {
  var tmp = null;
  if (target < 0) return;
  if (target === 0) return res.push(stack);
  for (var i = index; i < len; i++) {
    if (candidates[i] > target) break;
    tmp = Array.from(stack);
    tmp.push(candidates[i]);
    dfs(res, tmp, i, len, candidates, target - candidates[i]);
  }
};

```
***


## Combination Sum 2


>[문제](https://leetcode.com/problems/combination-sum-ii/)



### 내 답안


```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
  var res = [];
  var len = candidates.length;
  candidates.sort((a, b) => (a - b));
  dfs(res, [], 0, len, candidates, target);
  return res;
};

var dfs = function (res, stack, index, len, candidates, target) {
  var tmp = null;
  if (target < 0) return;
  if (target === 0) return res.push(stack);
  for (var i = index; i < len; i++) {
    if (candidates[i] > target) break;
    if (i > index && candidates[i] === candidates[i - 1]) continue;
    tmp = Array.from(stack);
    tmp.push(candidates[i]);
    dfs(res, tmp, i + 1, len, candidates, target - candidates[i]);
  }
};

```
***




## Permutations


>[문제](https://leetcode.com/problems/permutations/)



### 내 답안



```javascript

/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    
    var res=new Set();
    var curr=new Set();
    backtrack(res,curr,nums)
    return [...res];
    
};
var backtrack=function(res,curr,nums){
    if(nums.length===curr.size){ 
        res.add([...curr]);
    }else{
        for(var i=0;i<nums.length;i++){
            if(curr.has(nums[i])) continue;
            curr.add(nums[i]);
            backtrack(res,curr,nums);
            curr.delete(nums[i]);
        }
    }
}

```
***



## Permutations II


>[문제](https://leetcode.com/problems/permutations-ii/)



### 내 답안


```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    if(nums==null || nums.length===0) return nums;
    var res=new Set();
    var curr=[];
    var used=[];
    nums=nums.sort(function(a,b){ return a-b;})
    backtrack(res,used,curr,nums);
    return [...res];
};
var backtrack=function(res,used,curr,nums){
    if(curr.length===nums.length) {
        res.add([...curr]);
    }else {
        for(var i=0;i<nums.length;i++){
            if(used[i]) continue;
            if(i>0 && nums[i-1]===nums[i] && !used[i-1]) continue;
            curr.push(nums[i]);
            used[i]=true;
            backtrack(res,used,curr,nums);
            used[i]=false;
            curr.splice(curr.length-1,1);
        }
    }
}
```