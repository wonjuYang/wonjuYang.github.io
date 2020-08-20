---
title: "LinkedList"
categories: leetcode LinkedList
last_modified_at: 2020-08-09
---


# LinkedList



## reverseLinkedList


>[문제](https://leetcode.com/problems/add-two-numbers/)



### 내 답안

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
var reverseLinkedList = function(linkedlist) {
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



## Merge Two Sorted Lists


>[문제](https://leetcode.com/problems/merge-two-sorted-lists/)




### 내 답안
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
var mergeTwoLists = function(l1, l2) {
    
    let res = new ListNode(0);
    let head = res;
    let value = 0;

    while(l1 != null || l2 != null){
        
        if(l1 != null && l2 == null){
            head.next = new ListNode(l1.val);
            head = head.next
            l1 = l1.next
        }
        if(l2 != null && l1 == null){
            head.next = new ListNode(l2.val);
            head = head.next
            l2 = l2.next
        }
        
        if(l1 != null && l2 != null){
            if(l1.val<=l2.val){
                value = l1.val;
                l1 = l1.next;
            }else{
                value = l2.val;
                l2 = l2.next;
            }
            
            head.next = new ListNode(value);
            head = head.next;

        }
        
    }

    return res.next;
   
    
};

```
***

## Remove Nth Node From End of List


>[문제](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### 내 답안


```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */

var reverseLinkedList = function(linkedlist) {
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


var removeNthFromEnd = function(head, n) {

    
    head = reverseLinkedList(head);
    let tmp = new ListNode(0);
    let target_haed = tmp;
    
    if(head.next == null){
        return null;
    }
    
    if(n == 1 ){
        return reverseLinkedList(head.next)
    }
    
    
    for(let i = 0; i<n; i++){
        
        target_haed.next = new ListNode(head.val);
        target_haed = target_haed.next;
   
        head = head.next
        
        if(i==n-2){
            target_haed.next = head.next;
            target_haed = target_haed.next;
            break;
        }   
    } 
    return reverseLinkedList(tmp.next)
    

};
```

 