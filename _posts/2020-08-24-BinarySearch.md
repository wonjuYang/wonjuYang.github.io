---
title: "BinarySearch"
categories: leetcode BinarySearch
last_modified_at: 2020-08-24
---


# BinarySearch

## logn 

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



## Find First and Last Position of Element in Sorted Array


>[문제](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)



### 내 답안


```javascript

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
  var result = [];
  result[0] = findFirstIndex(nums, target);
  result[1] = findLastIndex(nums, target);

  return result;
};


function findFirstIndex(nums, target) {
  var index = -1;
  var start = 0;
  var end = nums.length - 1;
  while (start <= end) {
    var midPoint = Math.floor(start + (end - start) / 2);
    if (nums[midPoint] >= target) {
      end = midPoint - 1;
    } else {
      start = midPoint + 1;
    }

    if (nums[midPoint] === target) {
      index = midPoint;
    }
  }
  return index;
}

function findLastIndex(nums, target) {
  var index = -1;
  var start = 0;
  var end = nums.length - 1;
  while (start <= end) {
    var midPoint = Math.floor(start + (end - start) / 2);
    if (nums[midPoint] <= target) {
      start = midPoint + 1; //[start,end]=[0,2]
    } else {
      end = midPoint - 1;
    }

    if (nums[midPoint] === target) {
      index = midPoint;
    }
  }
  return index;
}

```