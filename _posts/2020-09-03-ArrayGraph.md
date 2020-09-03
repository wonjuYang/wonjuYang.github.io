---
title: "ArrayGraph"
categories: leetcode ArrayGraph
last_modified_at: 2020-09-03
---


# ArrayGraph



## Trapping Rain Water


>[문제](https://leetcode.com/problems/trapping-rain-water/)



### 내 답안


```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    if (!height || !height.length) {
        return 0;
    }
    
    let maxLeftWall = 0;
    let maxRightWall = 0;
    
    let water = 0;
    let i = 0;
    let j = height.length - 1;
    while (i < j) {
        if (height[i] < height[j]) {
            if (height[i] >= maxLeftWall) {
                maxLeftWall = height[i];
            } else {
                water += maxLeftWall - height[i];
            }
            i++;
        } else {
            if (height[j] >= maxRightWall) {
                maxRightWall = height[j];
            } else {
                water += maxRightWall - height[j];
            }
            j--;
        }
    }
    
    return water;
};
```
***
