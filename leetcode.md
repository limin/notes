### [1. Two Sum](https://leetcode.com/problems/two-sum/description/)
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
#### Asnwer
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

#### Answer
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

#### Answer
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

#### Answer
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
#### Answer
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
    while(l1!==null || l2!==null){ 
        if(l1===null){
            currentNode.next=l2
            break
        }else if(l2===null){
            currentNode.next=l1
            break
        }else{
            if(l1.val<l2.val){
                currentNode.next=l1 
                l1=l1.next 
            }else{
                currentNode.next=l2 
                l2=l2.next 
            }
        }
        currentNode=currentNode.next 
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

#### Answer
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

#### Answer
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

#### Answer
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

### [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/description/)
 Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6. 

#### Answer
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

### [66. Plus One](https://leetcode.com/problems/plus-one/description/)
Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

#### Answer
```javascript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    let addend=1,i=digits.length-1 //augend index
    while(addend>0 && i>=0){
        let result=digits[i]+addend
        if(result==10){
            digits[i--]=0            
        }else{
            digits[i]=result
            addend=0
        }
    }
    
    return i>=0?digits:[1,...digits]
};
```

### [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)
Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.

Example 1:
```
Input: 4
Output: 2
```
Example 2:
```
Input: 8
Output: 2
```
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated

#### Answer
```javascript
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function(x) {
    //r*r=x=>r-x/r=0=>r-x/r=delta=>r*r-x=d*r
    if(x===0) return 0
    let r=1
    while(true){
        let d=r-x/r
        if(d>=2 || d<=-2){
            r-=d/2 
        }else{
            r=Math.floor(r)
            return r*r>x?r-1:r
        }
    }
};
```


### [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```
Input: 2
Output:  2
```
Explanation:  There are two ways to climb to the top.
```
1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output:  3
```
Explanation:  There are three ways to climb to the top.
```
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

#### Answer
```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function(n) {
    //dynamic programming
    //f(n+2)=f(n)+f(n+1)
    let step1=1,step2=2,step=0    
    if(n===1) return 1
    if(n===2) return step2
    for(let i=3;i<=n;i++){
        step=step1+step2
        step1=step2
        step2=step
    }
    return step
};
```

### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

Answer
```javascript
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    let mi=m-1,ni=n-1
    while(mi>=0 || ni>=0){
        if(mi<0){
            nums1[mi+ni+1]=nums2[ni--]
        }
        else if(ni<0){
            nums1[mi+ni+1]=nums1[mi--]
        }else if(nums1[mi]>nums2[ni]){
            nums1[mi+ni+1]=nums1[mi--]
        }else{
            nums1[mi+ni+1]=nums2[ni--]
        }
    }    
};
```

### [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric: 
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
  2   2
   \   \
   3    3
```

#### Answer
Iterative
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function(root) {
    const nodes=[root]
    while(nodes.length>0){
        const len=nodes.length
        for(let i=0;i<len/2;i++){
            let pair=[nodes[i],nodes[len-1-i]]
            if((pair[0]===null && pair[1]!==null)||(pair[0]!==null && pair[1]===null)){
                return false
            }
            if((pair[0]!==null && pair[1]!==null) && pair[0].val!==pair[1].val){
                return false
            }
        }        
        for(let i=len;i>0;i--){
            const node=nodes.shift()
            if(node!=null){
                nodes.push(node.left)
                nodes.push(node.right)
            }

        }
    }
    return true
};
```

recursive
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function(root) {
    const isSymmetricPair=(left,right)=>{
        if(left===null && right===null){
            return true
        }else if(left===null||right===null){
            return false
        }else if(left.val!==right.val){
            return false
        }else{
            return isSymmetricPair(left.left,right.right)&&isSymmetricPair(left.right,right.left)
        }
    }
    if(root===null){
        return true
    }
    return isSymmetricPair(root.left,root.right)
};
```

### [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

#### Answer
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
    if(root==null) return 0
    return Math.max(1+maxDepth(root.left),1+maxDepth(root.right))
};
```
### [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
```
      0
     / \
   -3   9
   /   /
 -10  5
```

#### Answer
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function(nums) {
    function sortedSubArrayToBST(start,end,nums){
        const mid=Math.floor((start+end)/2)
        const root=new TreeNode(nums[mid])
        if(start<mid){
            root.left=sortedSubArrayToBST(start,mid-1,nums)
        }
        if(mid<end){
            root.right=sortedSubArrayToBST(mid+1,end,nums)
        }
        return root
    }    
    return nums.length===0?null:sortedSubArrayToBST(0,nums.length-1,nums)
};
```
### [118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/description/)
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```
#### Answer
```javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    //dynamic programming
    //fn=g(f(n-1))
    if(numRows<1) return []
    const triangle=[[1]]
    for(let i=1;i<numRows;i++){
        const lastRow=triangle[triangle.length-1]
        const newRow=[1]
        for(let j=0;j<lastRow.length-1;j++){
            newRow.push(lastRow[j]+lastRow[j+1])
        }
        newRow.push(1)
        triangle.push(newRow)
    }
    return triangle
};
```
### [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:
```
Input: [7, 1, 5, 3, 6, 4]
Output: 5
```
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:
```
Input: [7, 6, 4, 3, 1]
Output: 0
```
In this case, no transaction is done, i.e. max profit = 0.

#### Answer
```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    if(prices.length<=1) return 0
    let minPrc=prices[0], maxPrf=0
    for(let i=1;i<prices.length;i++){
        if(prices[i]<minPrc){
            minPrc=prices[i]
        }
        let profit=prices[i]-minPrc
        if(profit>maxPrf){
            maxPrf=profit
        }
    }
    return maxPrf
};
```

### [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

#### Answer
```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    //maxSellPofit, maxHoldProfit
    //maxSellProft[i]=maxHoldProfit+prices[i]:maxSellProfit
    //maxHoldProft[i]=maxSellProfit-prices[i]:maxHoldProfit
    if(prices.length<=1) return 0
    let maxSellProfit=0 //nothing happen
    let maxHoldProfit=-prices[0] 
    let max=Math.max(maxSellProfit,maxHoldProfit)
    for(let i=1;i<prices.length;i++){
        let sellProfit=Math.max(maxHoldProfit+prices[i],maxSellProfit)
        let holdProfit=Math.max(maxSellProfit-prices[i],maxHoldProfit)
        maxSellProfit=Math.max(maxSellProfit,sellProfit)
        maxHoldProfit=Math.max(maxHoldProfit,holdProfit)
        max=Math.max(max,maxSellProfit,maxHoldProfit)
    }    
    return max
};
```

### [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/)
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

#### Answer
```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    if(s===null || s.length===0) return true
    let i=0,j=s.length-1
    const isValidCode=(code)=>{
        return (code>="0".charCodeAt(0) && code<="9".charCodeAt(0)) || (code>='a'.charCodeAt(0) && code<='z'.charCodeAt(0))
    }
    s=s.toLowerCase()
    while(i<j){
        if(isValidCode(s.charCodeAt(i))&&isValidCode(s.charCodeAt(j))){
            if(s.charAt(i++)!==s.charAt(j--)) return false
        }
        if(!isValidCode(s.charCodeAt(i))) i++        
        if(!isValidCode(s.charCodeAt(j))) j--
    }
    return true
};
```

### [136. Single Number](https://leetcode.com/problems/single-number/description/)
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

#### Answer
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    if(nums.length===0) throw "Invalid argument"
    let single=nums[0]
    for(let i=1;i<nums.length;i++){
        single=single ^ nums[i]
    }
    return single
};
```

### [412. Fizz Buzz](https://leetcode.com/problems/fizz-buzz/description/)
Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

#### Answer
```javascript
/**
 * @param {number} n
 * @return {string[]}
 */
var fizzBuzz = function(n) {
    let output=[]
    for(let i=1,fizz=1, buzz=1;i<=n;i++,fizz++,buzz++){
        if(fizz===3 && buzz===5){
            output.push("FizzBuzz")
            fizz=0  
            buzz=0
        }else if(fizz===3){
            output.push("Fizz")
            fizz=0
        }else if(buzz===5){
            output.push("Buzz")
            buzz=0
        }else{
            output.push(new String(i))            
        }
    }
    return output
};
```
### [387. First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/description/)
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

Examples:
```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```
Note: You may assume the string contain only lowercase letters.

#### Answer
```javascript
/**
 * @param {string} s
 * @return {number}
 */
var firstUniqChar = function(s) {
    if(s===null || s.length===0) return -1
    const counters=[], a='a'.charCodeAt(0),z='z'.charCodeAt(0)
    for(let i=0;i<=z-a;i++){
        counters[i]=0
    }
    for(let i=0;i<s.length;i++){
        counters[s.charCodeAt(i)-a]++
    }
    for(let i=0;i<s.length;i++){
        if(counters[s.charCodeAt(i)-a]===1) return i
    }
    return -1
};
```

