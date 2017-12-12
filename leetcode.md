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
