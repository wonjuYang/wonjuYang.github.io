---
title: "LinkedList"
categories: leetcode LinkedList
last_modified_at: 2020-08-09
---


## LinkedList



> reverseLinkedList




>> [문제](https://leetcode.com/problems/add-two-numbers/)





>>> 내 답안

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var reverseLinkedList = Afunction(linkedlist) {
  var node = linkedlist;
  var previous = null;

  while(node) {
    // save next or you lose it!!!
    var save = node.next;
    // reverse pointer
    node.next = previous;
    // increment previous to current node
    previous = node;
    // increment node to next node or null at end of list
    node = save;
  }
  return previous;   // Change the list head !!!
}

var addTwoNumbers = function(l1, l2) {
   
    var List = new ListNode(0);
    var head = List;
    var sum = 0;
    var carry = 0;
    
    while(l1!==null || l2!==null || sum >0){
        
        if(l1!==null){
            sum += l1.val;
            l1 = l1.next;
        }
        
        if(l2!==null){
            sum += l2.val;
            l2 = l2.next;
        }
        
        if(sum>=10){
            carry = 1;
            sum -= 10;
        }
        
        head.next = new ListNode(sum);
        head = head.next;
        
        sum = carry;
        carry = 0;
        
        
    }
    
        return List.next;


};
```


***
***
***