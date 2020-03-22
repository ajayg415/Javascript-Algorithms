# Javascript-Algorithms
---

###### 1. Write an algoritm for the below problem statement.

```
 There are 8 houses in a row. Some houses are empty and some are not, it will be represented with 1 and 0. 
 
 On Day 1 lets say first 3 house are atcive so it will be represented like 111, 
 
 - on day 2 for first house his neighbours are empty(0) and active(1) on previous day so he will be active (1), 
 - for 2nd house both neighbours are active(1) on previous day so he will be passive (0)
 - for house 3 house his beighbours are active(1) and empty (0), so he will be active (1). 
 
 So day 2 status for first 3 houses will be 101.  
 
Example:

Day 1-> 1 0 1 1 0 0 1 0
Day 2-> 0 0 1 1 1 1 0 1
Day 3-> 0 1 1 0 0 1 0 0
Day 4-> 1 1 1 1 1 0 1 0
Day 5-> 1 0 0 0 1 0 0 1

Now, Write a algorithm to find out the status of each house on any given day and status of houses on Day 1. 
Example: findStatus([1,1,1,0,1,0,1,0], 5)
```


<details>
<summary>Answer...</summary>
<p>

```
 const findStatus = (arr, day) =>{
  return (day === 1) ? arr : findStatus(checkStatus(arr), day-1);
 };
 
 const checkStatus = arr => {
  return arr.reduce((a,c,i)=>{
    return (arr[i-1] === arr[i+1]) ? [...a, 0] : [...a, 1]
  },[]) 
 };
 
 findStatus([1,1,1,0,1,0,1,0], 5)
```

</p>
</details>  
