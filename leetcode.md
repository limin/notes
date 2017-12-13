### [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
Asnwer:
```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    for(let i=0;i<nums.length;i++){
        for(var j=i+1;j<nums.length;j++){
            if(nums[j]===target-nums[i]){
               return [i,j]
               }
        }
    }
    return []
};
```

### [7. Reverse Integer ](https://leetcode.com/problems/reverse-integer/description/)
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:
```
Input: 123
Output:  321
```
Example 2:
```
Input: -123
Output: -321
```
Example 3:
```
Input: 120
Output: 21
```
Note:
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows. 

Answer:
```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    if(x===0) return 0
    const MAX=Math.pow(2,31)
    const sign=x>0?1:-1    
    let result=0,digit=0
    x=sign*x
    while(x>0){
        digit=x % 10
        if(MAX-digit<result*10){
            return 0   
        }
        result=result*10+digit
        x=Math.floor(x/10)
    }
    return result==MAX&&sign==-1?0:sign*result
};
```

### [14. Longest Common Prefix ](https://leetcode.com/problems/longest-common-prefix/description/)
Write a function to find the longest common prefix string amongst an array of strings. 

Answer:
```javascript
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function(strs) {
    if(strs.length==0)
        return ""
    let i=-1,completed=false
    while(!completed){
        let c=null
        i++
        for(let str of strs){
            if(i>=str.length){
                completed=true
                break;
            }
            if(c===null){
                c=str.charAt(i)
            }else if(c!==str.charAt(i)){
                completed=true
                break;
            }
        }
    }
    return strs[0].substring(0,i)
};
```

### [20. Valid Parentheses ](https://leetcode.com/problems/valid-parentheses/description/)
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

Answer:
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    let pairs=[] 
    for(let i=0;i<s.length;i++){ //s="([])", i=1
        switch(s.charAt(i)){ //]
            case '(':
                pairs.push(')')
                break
            case '{':
                pairs.push('}')
                break
            case '[':
                pairs.push(']') //pairs=]
                break
            case ')':
            case '}':
            case ']':
                if(pairs.length>0 && pairs.pop()===s.charAt(i)){
                    // do nothing
                }else{
                    return false
                }
        }
    }
    return pairs.length===0
};
```

### [ 21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
Answer:
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    const mergedList=new ListNode(null)
    let currentNode=mergedList
    while(l1!==null || l2!==null){ //4, >3->4
        if(l1===null){
            currentNode.next=l2
            l2=l2.next
        }else if(l2===null){
            currentNode.next=l1
            l1=l1.next
        }else{
            if(l1.val<l2.val){
                currentNode.next=l1 //null->1->1->2
                l1=l1.next //4
            }else{
                currentNode.next=l2 //null->1
                l2=l2.next //1->2->4,3->4
            }
        }
        currentNode=currentNode.next //1->1->2
    }
    return mergedList.next
};
```

### [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
 Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example:
```
Given nums = [1,1,2],
```
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.

Answer:
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {    
    let i=0, len=nums.length
    for(let j=1;j<len;j++){
        if(nums[i]!==nums[j]){
            nums[++i]=nums[j]
        }
    }

    return i+1
};
```

### [28. Implement strStr()](https://leetcode.com/problems/implement-strstr/description/)
 Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:
```
Input: haystack = "hello", needle = "ll"
Output: 2
```
Example 2:
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

Answer:
```javascript
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
    if(haystack === null || needle === null){
        return -1
    }
    
    for(let i=0;i<haystack.length;i++){
        if(haystack.length-i<needle.length){
            return -1
        }
        let matched=true
        for(let j=0;j<needle.length;j++){
            if(needle.charAt(j)!==haystack.charAt(j+i)){
                matched=false
            }
        }
        if(matched){
            return i
        }
    }
    return needle.length===0?0:-1
};
```

### [38. Count and Say](https://leetcode.com/problems/count-and-say/description/)
The count-and-say sequence is the sequence of integers with the first five terms as following:
```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

Example 1:
```
Input: 1
Output: "1"
```
Example 2:
```
Input: 4
Output: "1211"
```

Answer:
```javascript
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
    const count=(say)=>{
        let result=""
        let counter={digit:null,count:0}
        for(let i=0;i<say.length;i++){
            if(say.charAt(i)===counter.digit){
                counter.count++
            }else{
                if(counter.digit!==null){
                    result=result.concat(counter.count).concat(counter.digit)
                }
                counter={digit:say.charAt(i),count:1}
            }
        }
        result=result.concat(counter.count).concat(counter.digit)
        //console.log(result)        
        return result
    }
    let say="1"
    for(let i=2;i<=n;i++){
        say=count(say)
    }
    return say
};
```

### [53. Maximum Subarray ?](https://leetcode.com/problems/maximum-subarray/description/)
 Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6. 

Answer:
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    if(nums.length===0){
        return 0
    }
    //dynamic programming.
    //f(i)=f(i-1)>0?f(i-1)+nums[i]:nums[i]
    //f(0)=nums(0)
    //maxi: the max sum of the sub array end with index i
    let max=nums[0], maxi=nums[0]
    for(let i=1;i<nums.length;i++){
        maxi=maxi>0?maxi+nums[i]:nums[i]
        if(maxi>max){max=maxi}
    }
    return max
};
```
