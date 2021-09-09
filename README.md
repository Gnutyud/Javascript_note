# Javascript_note
Note some helpful piece of code in javascript.
My list :
- [Minimum number of bottles required to fill K glasses](#minimum-number-of-bottles-required-to-fill-k-glasses)
- [Shortest substring occurring only once in a given string](#shortest-unique-substring-occurring-only-once-in-a-given-string)
##  Minimum number of bottles required to fill K glasses
There are N empty glasses with a capacity of 1,2,…,N liters(there is exactly one glass of each unique capacity)
You want to pour exactly K liters of water into glasses.
Each glass may be either full or empty(a glass cannot be partially filled).
What is the minimum number of glasses that you need to contain K liters of water?
```js
function minimumGlasses(N, K) {
  let result = [];
  let sumN = (N * (N + 1)) / 2;
  if (K <= N) return 1;
  if (K > sumN) return -1;
  if (sumN === K) return N;
  getListResult(K);
  function getListResult(remain) {
    let min = Math.min(remain, N);
    for (let i = min; i > 0; i--) {
      if (!result.includes(i)) {
        result.push(i);
        remain -= i;
        return getListResult(remain);
      }
    }
  }
  return result.length;
}
console.log(minimumGlasses(5, 8));
```
## Shortest unique substring occurring only once in a given string
Given a string S consisting of N lowercase alphabets, the task is to find the length of the shortest unique substring in S whose occurrence is exactly 1.
```js
function uniqueShortestSubString(string) {
  let str = string.toLowerCase();
  let allSubStr = [];
  let uniqueStr = [];
  let shortest;
  // get all substring
  for (let i = 0; i < str.length; i++) {
    for (let j = i + 1; j <= str.length; j++) {
      if (i != j) {
        allSubStr.push(str.substring(i, j));
      }
    }
  }
  // get unique substring
  for (let i = 0; i < allSubStr.length; i++) {
    let allSubStrCopy = [...allSubStr];
    allSubStrCopy.splice(i, 1);
    if (!allSubStrCopy.includes(allSubStr[i])) {
      uniqueStr.push(allSubStr[i]);
    }
  }
  // get shortest unique substring
  shortest = Math.min(...uniqueStr.map(({ length }) => length));
  // check substring shortest and unique
  return shortest;
  }
