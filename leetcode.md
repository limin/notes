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
