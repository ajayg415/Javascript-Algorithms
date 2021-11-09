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
Solution 1:
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


Solution 2:
function getNmatrix (data) {
  if(data.length<=1){return data;}
  var len = Math.ceil(Math.sqrt((data.length)));
  var arr = [...data, ...new Array((len*len)-data.length).fill(0)];
  var result = [];
  
  for(var i=0;i<len;i++){
    result.push(arr.slice((i*len), ((i*len)+len)));
  }
  return result;
}
```
</p>
</details>

###### 7. Write a program for grouping the Objects based on given properties
```js
Input: var array = [
  { Id: "001", qty: 1, proj: 'A'}, 
  { Id: "002", qty: 2, proj: 'A'}, 
  { Id: "001", qty: 2,proj: 'B'}, 
  { Id: "003", qty: 4, proj: 'C' },
  { Id: "001", qty: 4, proj: 'B' }
];

Ouput:
[{Id: "001", qty: 1, proj: "A"},
{Id: "002", qty: 2, proj: "A"},
{Id: "001", qty: 6, proj: "B"},
{Id: "003", qty: 4, proj: "C"}]

```
<details>
<summary>Answer...</summary>
<p>
 
 ```js
let groupyByKeys = (arr, keysarray) => {
   let result = []
   let temp = arr.reduce( (res, value) => {
   let key = ''; 
   for(var i of keysarray){ key = key + value[i] }
   
	  if(!res[key]){
     res[key] = { Id:value.Id , qty: 0 , proj: value.proj};
     result.push(res[key])
	  }
	  res[key].qty += value.qty;
	  return res;
   }, {});
   console.log(result)
}

groupyByKeys(array, ['Id', 'proj'])
 
 ```

</details>


###### 8. Write a program for getting the given key occurrences in the object
```js

Example

Input
srcObj = { a: 3, b: 4, c: { f: 3, d: 5 }, m: { f: 4 }, d: { g: { f: 6 }, f: 7 } };
key = 'f' 

Output:
4
```
<details>
<summary>Answer...</summary>
<p>
	
 ```js
  let getAllKeysCount = (obj, desired) => {
   let objkeys = [];
   let getKeys = (obj) => {
     for(var key in obj){
       objkeys.push(key);
       if(typeof obj[key] === 'object'){
          getKeys(obj[key])
       }
     }
     return objkeys.reduce( (acc, curr) =>{
       if(curr === desired) {
        acc++;
       }
       return acc;
     }, 0)
   }
   return getKeys(obj)
 }

  var srcObj = { a: 3, b: 4, c: { f: 3, d: 5 }, m: { f: 4 }, d: { g: { f: 6 }, f: 7 } };
  getAllKeysCount(srcObj, 'd') // 2
  getAllKeysCount(srcObj, 'f') // 4 
 ```
</details>

###### 9. Sum of Two
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.
```js

Example

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

var twoSum = function(nums, target){
  //Code goes here
}
```
<details>
<summary>Answer...</summary>
<p>
	
 ```js
var twoSum = function(nums, target) {
  for(let i=0;i<nums.length;i++){
    const num = target-nums[i]
    if(nums.includes(num)){
      return [i, nums.indexOf(num)]
    }
  }
}
 ```
</details>


###### 10. Sort the unsorted Array 
We have one unsorted array with duplication.
Write a logic to sort the array like below.

```js

Input =  [1, 5, 2, 1, 5, 2, 3, 5, 5, 1];

Output = [1, 2, 3, 5, 1, 2, 5, 1, 5, 1];

hint: [[1,2,3,5], [1,2,5], [1,5], [1]]
```
<details>
<summary>Answer...</summary>
<p>
	
 ```js
var resTempArr = []
var count = 0;
var arr = [1, 5, 2, 1, 5, 2, 3, 5, 5, 1];
var sortedArr = arr.sort((a,b) => a-b)
for(var i = 0; i< sortedArr.length;i++){
 if(sortedArr[i]== sortedArr[i-1]){
    count++;
    if(!resTempArr[count]) 
       resTempArr[count] = []
    resTempArr[count].push(sortedArr[i])    
 }
 if(sortedArr[i]!= sortedArr[i-1]){
     count = 0;
     if(!resTempArr[count]) 
        resTempArr[count] = []
     resTempArr[count].push(sortedArr[i])
  }
}
console.log(resTempArr.flat())
 ```
</details>

###### 11. There's an algorithms tournament taking place in which teams of programmers compete against each other to solve algorithmic problems as fast as possible. Teams compete in a round robin, where each team faces off against all other
teams. Only two teams compete against each other at a time, and for each competition, one team is designated the home team, while the other team is the away team. In each competition there's always one winner and one loser; there
are no ties. A team receives 3 points if it wins and 0 points if it loses. The winner of the tournament is the team that receives the most amount of points.

Given an array of pairs representing the teams that have competed against each other and an array containing the results of each competition, write a function that returns the winner of the tournament. The input arrays are named competitions and results, respectively. The competitions array has elements in the form of [homeTown, awayTown] , where each team is a string of at most 30 characters representing the name of the team. The results array contains information about the winner of each corresponding competition in the competitions array. Specifically results[i] denotes the winner of competitions[i], where a 1 in the results array means that the home team in the corresponding competition won and a 0 means that the away team won.

It's guaranteed that exactly one team will win the tournament and that each team will compete against all other teams exactly once. It's also guaranteed that the tournament will always have at least two teams.

refer <a href="https://github.com/ajayg415/Javascript-Algorithms/issues/18">for more details</a>

```js

Sample Input
const competitions = [
  ["HTML", "C#"],
  ["C#", "Python"],
  ["Python", "HTML"],
];
const results = [1, 0, 0]

Sample Output:  "Python"
// C# beats HTML, Python Beats C#, and Python Beats HTML.
// HTML - 0 points 
// C# -  3 points
// Python -  6 points
```
<details>
<summary>Answer...</summary>
<p>
  
 ```js
function tournamentWinner(matchSchedule, results) {

  const winnersObj = {}; let winnerTeam = '', winnerPoints = 3;

  // reduce loop runs 'n' times so the complexity of it is O(n)
  winnerTeam = results.reduce((wTeam, result, ind) => {
    const eachMatchWinner = result ? competitions[ind][0] : competitions[ind][1];
    
    //below if/else condition runs for every n item so the complexity become
    // O(n+1)
    if(!winnersObj[eachMatchWinner]) {
      winnersObj[eachMatchWinner] = 3;
    
    } else {
      winnersObj[eachMatchWinner] = winnersObj[eachMatchWinner] + 3;
      //Need to add this if condition also to complexity of the function
      if(winnersObj[eachMatchWinner] > winnerPoints) {
        wTeam = eachMatchWinner
      }
    }
    return wTeam;
    
  }, winnerTeam);

  return winnerTeam;
}

console.log(tournamentWinner(competitions, results));
 ```
</details>


###### 12. Array Of Products: Write a function that takes in a non-empty array of integers and returns an array of the same length, where each element in the output array is equal to the product of every other number in the input array.

In other words, the value at output[i] is equal to the product of every number in the input array other than input[i].

Note that you're expected to solve this problem without using division.

<h3>Sample Input</h3>
<pre>array = [5, 1, 4, 2] </pre>
<h3>Sample Output</h3>
<pre>[8, 40, 10, 20]
// 8 is equal to 1 x 4 x 2
// 40 is equal to 5 x 4 x 2
// 10 is equal to 5 x 1 x 2
// 20 is equal to 5 x 1 x 4
</pre>

> _O(n) time | O(n) space - where n is the length of the input array_
```js

Sample Input
const competitions = [
  ["HTML", "C#"],
  ["C#", "Python"],
  ["Python", "HTML"],
];
const results = [1, 0, 0]

Sample Output:  "Python"
// C# beats HTML, Python Beats C#, and Python Beats HTML.
// HTML - 0 points 
// C# -  3 points
// Python -  6 points
```
<details>
<summary>Answer...</summary>
<p>
	
 ```js
function arrayOfProducts(array) {
  let res = [];
  for(let i=0;i<array.length;i++){
    res.push(array.reduce((a,c, ind) => ((ind === i ? a*1 : c*a)), 1))
  }
  return res;
}
```
> _Time Complexity: O(n^2) and Space complexity O(n)_
</details>




###### 12. Non-Constructible Change:   Given an array of positive integers representing the values of coins in your possession, write a function that returns the minimum amount of change (the minimum sum of money) that you **cannot**  create. The given coins can have any positive integer value and aren't necessarily unique (i.e., you can have multiple coins of the same value).

  For example, if you're given `coins = [1, 2, 5]`, the minimum amount of change that you can't create is `4`. If you're given no
  coins, the minimum amount of change that you can't create is '1'

> _Note: O(nlogn) time | O(1) space - where n is the number of coins_

```js
Sample Input: 
Coins:  = [5, 7, 1, 1, 2, 3, 22]
Sample Output: 20
```

```js
function nonConstructibleChange(coins) {
  // Write your code here.
  return 1;
}
```
<details>
<summary>Answer...</summary>
<p>

```js	
function nonConstructibleChange(coins) {
  coins.sort((a,b) => (a-b))
  let storedVal = 0
  for(const coin of coins){
    if( coin > storedVal +1) return storedVal + 1;
      storedVal += coin;
    }
  return storedVal+1
}
```
</details>
