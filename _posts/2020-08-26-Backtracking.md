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
//Backtracking
var combinationSum = function(candidates, target) {
        let res=[];
        let list=[];
        candidates.sort((a,b)=>a-b);
        backTrack(res,list,candidates,target,0);
        return res;
}
var backTrack=function(res,list,candidates,target,start){
        if(target>0){
            for(let i=start; i<candidates.length && target>=candidates[i]; i++){
                list.push(candidates[i]);
                backTrack(res,list,candidates,target-candidates[i],i);
                list.pop();
            }
        }else if(target==0){
            res.push([...list]);
        }
}

```