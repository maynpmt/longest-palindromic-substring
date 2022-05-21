## Problem
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1: 
```
Input: "babad"
Output: "bab" 
Note: "aba" is also a valid answer.
```

Example 2: 
```
Input: "cbbd" 
Output: "bb" 
```
## Solution
```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  let start = 0;
  let end = 0;
  let longestLength = 0;

  //check if string length <= 1000
  if(s.length <= 1000){
    // Loop through the letters
    for(let i=0; i<s.length; i++){
      //find  new longest length
      longestLength = Math.max(expandAroundCenter(s, i, i), expandAroundCenter(s, i, i + 1)); //compare between the center is letter and the center is between two letters
      // compare between current and new longest 
      if(longestLength > end - start){ 
        start = i - Math.floor((longestLength-1) / 2); //find new start position (center position - (longestLength-1)/2)
        end = i + Math.floor(longestLength / 2) //find new end position (center position + (longestLength)/2)
      }
    }
    return s.slice(start, end + 1);   
  }
  return null
};

var expandAroundCenter = function(s, leftPos, rightPos) {
  while(leftPos >= 0 && rightPos < s.length && s[leftPos] === s[rightPos]){
    //expand in each direction
    leftPos--;
    rightPos++;
  }
  return rightPos - leftPos - 1;
}
```
