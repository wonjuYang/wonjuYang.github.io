---
title: "BinarySearch"
categories: leetcode BinarySearch
last_modified_at: 2020-08-24
---


# BinarySearch



## Search in Rotated Sorted Array


>[문제](https://leetcode.com/problems/search-in-rotated-sorted-array/)



### 내 답안

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {

        let l = 0;
        let r = nums.length - 1;
        
        while(l <= r) {
            let mid = (l + r) >> 1;
            
            if(nums[mid] == target) return mid;
            else if(nums[mid] > target) {
                if(nums[r] < nums[mid] && target <= nums[r]) l = mid + 1;
                else r = mid - 1;
            } else {
                if(nums[mid] < nums[l] && target >= nums[l]) r = mid - 1;
                else l = mid + 1;
            }
        }
        
        return -1;

};
```
***