# Javascript Algorithms
---

###### 1. Write an algorithm for the below problem statement.


 There are 8 houses in a row. Some houses are empty and some are not, it will be represented with 1 and 0. 
 
 On Day 1 let’s say first 3 houses are active so it will be represented like [1 1 1], 
 
 On day 2
 - For 1st house, his neighbors are empty (0) and active (1) on previous day so he will be active (1), 
 - For 2nd house, both neighbors are active (1) on previous day so he will be passive (0)
 - For 3rd house, his neighbors are active (1) and empty (0) on previous day, so he will be active (1). 
 
 So day 2 status for first 3 houses will be [1 0 1].  
 
Example:
```js
Sample Input:  [1 0 1 1 0 0  1 0]
Sample Day 1 Output -> [1 0 1 1 0 0 1 0]
Sample Day 2 Output -> [0 0 1 1 1 1 0 1]
Sample Day 3 Output -> [0 1 1 0 0 1 0 0]
Sample Day 4 Output -> [1 1 1 1 1 0 1 0]
Sample Day 5 Output -> [1 0 0 0 1 0 0 1]
```
Now, write an algorithm to find out the status of each house on any given day. 
Example: findStatus([1,1,1,0,1,0,1,0], 5)




<details>
<summary>Answer...</summary>
<p>

```js
const findStatus = (arr, day) =>{
 return (day === 0) ? arr : findStatus(checkStatus(arr), day-1);
};
 
const checkStatus = arr => {
 return arr.reduce((a,c,i)=>{
   return (arr[i-1] === arr[i+1]) ? [...a, 0] : [...a, 1]
 },[]) 
};
 
findStatus([1,1,1,0,1,0,1,0], 5) = > output: [1, 0, 1, 0, 1, 0, 0, 1]
```

</p>
</details>  

###### 2. Write an algorithm to remove all duplicates and non repeated values from an array.

```js
Sample Input:  [1, 1, 2, 3, 3, 3, 4, 2, 5, 5]
Sample output: [1, 2, 3, 5] (4 not repaeated in the output array)
```

<details>
<summary>Answer...</summary>
<p>

```js
const getArray = arr => arr.sort((a,b)=>(a-b)).reduce((a,c,i,ar)=>{
  return (!a.includes(c) && (ar[i-1] === c || ar[i+1] === c)) ? [...a, c] : [...a]
},[])
```

In the above code apart for checking unique values using array reducer, 
we're also checking if the main array previous or next index has same values. 
This way we can includes only repeated values from main array.

</p>
</details>

###### 3. Write a program for binary search pattern.

Binary match pattern is kind of search which returns the number of times the pattern is matched 
in a given string.

Write a function which returns the number of times the pattern is matched in a given string. 
The pattern will be in binary format meaning combination of 0 and 1's.

Rules: if the number is 0 in the pattern then it should be vowel and if the number is 1 then 
it should be consonant. Searching string will be of lower case only and will be of one word only.
Pattern will be in a string.

Example 1: :
Input : Pattern: '010', Search String: 'amazing'
Output: 2

Explanation: In the above pattern first and last numbers are zero's so the letters should start and end 
with vowel and as the second number is 1, the middle letter is consonant. So the function should search 
for such kind of words in the word and return the count. In the above given input it matches only twice 
and they are:
'ama'
'azi'
Example 2:
Input: Pattern: 100, Search String : 'seesaw'
Output: 1

Matches are:
'see'

```js
function binaryMatchPattern(searchString, pattern) {
  //code goes here 
}
```

<details>
<summary>Answer...</summary>
<p>

Solution 1: 
```js
 function binaryMatchPattern(searchString, pattern){
     let i = searchString.length;
     const searchStringLength = i;
     const patternLength = pattern.length;
     let updatedPattern = pattern
                            .replace(/0/g, '[aeiou]')
                            .replace(/1/g, '[b-df-hj-np-tv-z]');
     const patternToMatch = new RegExp(updatedPattern);
     let matchingItems = 0;
     
     while(i >= patternLength) {
        const slicedString = searchString.substr(searchStringLength - i, patternLength);
        
        // Below code is saving the matched items. but we dont need it hence commenting it.
        //patternToMatch.test(slicedString) && matchingItems.push(slicedString);
        
        patternToMatch.test(slicedString) && matchingItems++
        i--;
     }
     return matchingItems;
 }
```

Take away points:
- We are dynamically creating the regexp using the Regular Expression constructor.
- Leveraging the build in methods instead of creating our own methods for looping and matching.

Soltion 2:
```js
const getBoolean = str => {
  // returns Boolean representation of given string. Ex: Amazon => 010101
  return str.replace(/[^aeiou]/g,'1').replace(/[aeiou]/g,'0'); 
}

const binaryMatchPattern = (searchString, pattern) => {
  const len = pattern.length;
 
  return searchString.split('').reduce((a,c,i)=>{
   const subStr = searchString.substr(i-1, len);
   return (subStr.length === len && getBoolean(subStr) === pattern) ? (a +1) : a;
  }, 0)
}

```


</p>
</details>

###### 4. Write a program for the given string is a balanced string or not


If the orders of “{“,”}”,”(“,”)”,”[“,”]” are correct in a string is called Balanced string.
```js
Example 1:  '[{[({})]}]'
output: true

Example 2: '[{}()]' 
output: true

Example 3: '[{()]'
output: true
```
<details>
<summary>Answer...</summary>
<p>
 
```js
Solution:
var a = '[{[({})]}]';
var b = '[{}()]';
var c = '[{()]';

function isBalancedString(abc){
  var flag = true;
  var obj = {
    ']': '[',
    ')' : '(',
    '}' : '{'
  }
  var stack = [];
  for(var k = 0; k < abc.length;k++) {
      if(abc[k] === '{' || abc[k] === '[' || abc[k] === '(') {
         stack.push(abc[k])
      }else{
         if(obj[abc[k]] === stack[stack.length-1]){
          stack.pop();
         }
      }    
  }
  return stack.length === 0 ? true: false
}

isBalancedString(a) // true
isBalancedString(b) // true
isBalancedString(c) // false
```
</p>
</details>


###### 5. Write a program for finding the square root of a given number

The below mentioned solution is not going to be accurate with `Math.sqrt` result. An attempt to
get the desired result. But if you have any solution which gives more accurate results, you are welcome
to issue a PR and your solution will be placed over here. 

```js
Input:  9
output: 3

Input: 544 
output: 23.32

Input: 90
output: 9.48
```
<details>
<summary>Answer...</summary>
<p>
 
```js
Solution:
function getSquareRoot(a){
    let result = Math.ceil(a/2);
    let updateClosestSqValue;
    let sqOfresult = result * result;
    
    while(sqOfresult > a) {
        result = Math.ceil(result/2);
        sqOfresult = result * result;
    }
    let closestSqValue = result/2;
    updateClosestSqValue = result + closestSqValue;
    
    while ((updateClosestSqValue*updateClosestSqValue) > a) {
        updateClosestSqValue = result + (closestSqValue/2);
        closestSqValue = closestSqValue/2
    }
    
    let finalSqValue = result + closestSqValue;
        
    while( (finalSqValue*finalSqValue) < a) {
     result = finalSqValue;
      finalSqValue = finalSqValue + 0.01;     
    }

    return result;
}

getSquareRoot(9) // 3
getSquareRoot(544) // 23.32
getSquareRoot(90) // 9.47
```
</p>
</details>

###### 6. Write a program for generation of N*N matrix for the given data set

 

```js
Input:  [9]
Output: [9]

Input: [4,5]
Output: [[4,5],[0,0]]

Input: [4,5,6]
Output: [[4,5],[6,0]]

Input: [5,6,7,8,9]
Output: [[5,6,7],[8,9,0],[0,0,0]]
```
<details>
<summary>Answer...</summary>
<p>
 
```js
Solution:
function getNmatrix (data) {
 let dataLength = data.length;
 let isNdetermined = false;
 let n = 1;
 let result = [];
 let cachedN = n;

 if (data.constructor.name !== "Array") {
    return "Provided data argument is not of type array";
 }

 if (dataLength <= 1) {
  return data;
 }
 
 while (n > 0 ) {
    if(!isNdetermined) {
        n = n+1;
        isNdetermined = (n*n) >= dataLength; 
        cachedN = n;
    } else {
        if(dataLength >= cachedN){
            result.push(data.splice(0, cachedN));
        } else {
            const zeroArray = new Array(cachedN-dataLength).fill(0, 0);
            result.push([...data.splice(0,cachedN), ...zeroArray]);
        }
            
        dataLength = data.length;
        n = n-1;
    }
 }
  return result;
}
getNmatrix([9]) // [9]
getNmatrix([4,5]) // [[4,5],[0,0]]
getNmatrix([4,5,6]) // [[4,5],[6,0]]
```
</p>
</details>

