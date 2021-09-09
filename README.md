# Javascript_note
Some helpful piece of code in javascript of mine :
- [Minimum number of bottles required to fill K glasses](#minimum-number-of-bottles-required-to-fill-k-glasses)
- [Shortest substring occurring only once in a given string](#shortest-unique-substring-occurring-only-once-in-a-given-string)
- [Minimum number of steps required to make all elements equal in array](#minimum-number-of-steps-required-to-make-all-elements-equal-in-array)
- [Is there exists a path from vertex 1 to N going through all vertices in an undirected graph](#is-there-exists-a-path-from-vertex-1-to-n-going-through-all-vertices-in-an-undirected-graph)
- [Get search results from the save contacts for the number you entered](#get-search-results-from-the-save-contacts-for-the-number-you-entered)
- [Count of different numbers divisible by 3 that can be obtained by changing at most one digit](#count-of-different-numbers-divisible-by-3-that-can-be-obtained-by-changing-at-most-one-digit)
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
  ```
## Minimum number of steps required to make all elements equal in array
Any element of a given array can be either increased or decreased by 1.
```js
function makeAllEqual(arr) {
  let countStep = 0;
  //   create an Object to count duplicte element in arr
  let countDulicateElement = {};
  arr.forEach((element) => {
    countDulicateElement[element] = (countDulicateElement[element] || 0) + 1;
  });
  // get arr sorted and unique
  let uniqueArr = new Set(arr);
  let uniqueSortArr = [...uniqueArr].sort();
  //   if all element already equals return 0
  if (uniqueSortArr.length === 1) {
    return 0;
  }
  let averageNum = Math.round(
    arr.reduce((prev, curr) => prev + curr) / arr.length,
  );
  console.log(averageNum);
  //   count step needed
  for (let i = 0; i < uniqueSortArr.length; i++) {
    if (uniqueSortArr[i] !== averageNum) {
      countStep +=
        uniqueSortArr[i] > averageNum
          ? (uniqueSortArr[i] - averageNum) *
            countDulicateElement[uniqueSortArr[i]]
          : (averageNum - uniqueSortArr[i]) *
            countDulicateElement[uniqueSortArr[i]];
    }
  }
  return countStep;
}
```
## Is there exists a path from vertex 1 to N going through all vertices in an undirected graph
You are given an undirected graph consisting of N vertices, numbered from 1 to N, and M edges. The graph is described by two arrays, A and B, both of length M. A pair (A[K], B[K]), for K from 0 to M-1, describes an edge between vertex A[K] and vertex B[K]. Your task is to check whether the given graph contains a path from vertex 1 to vertex N going through all of the vertices, one by one, in increasing order of their numbers. All connections on the path should be direct.
```js
function isAPath(arr1, arr2, N) {
  let allVector = [];
  let pathVectorList = [];
  for (let i = 0; i < arr1.length; i++) {
    allVector.push(`${arr1[i]}${arr2[i]}`);
  }
  console.log(allVector);
  // check every vector in allVector must not self-loop and no multiple egdes between same vectors
  if (allVector.length !== new Set(allVector).size) {
    console.log("The Graph has multiple egdes between same vectors");
    return false;
  }
  for (let i = 0; i < allVector.length; i++) {
    if (allVector.includes(reverseString(allVector[i]))) {
      console.log(
        `There are a self-loop in the graph at vector ${allVector[i]}`,
      );
      return false;
    }
  }
  // get the path in graph from 1 to N
  for (let i = 1; i < N; i++) {
    if (i !== N) {
      pathVectorList.push(`${i}${i + 1}`);
    }
  }
  console.log(pathVectorList);
  // check is a path from 1 to N from allVector
  for (let i = 0; i < pathVectorList.length; i++) {
    if (
      !allVector.includes(pathVectorList[i]) &&
      !allVector.includes(reverseString(pathVectorList[i]))
    ) {
      console.log("not include", pathVectorList[i]);
      return false;
    }
  }
  return true;
  // function reverseString
  function reverseString(str) {
    return str === "" ? "" : reverseString(str.substr(1)) + str.charAt(0);
  }
}
```
## Get search results from the save contacts for the number you entered
Task Description:

When you open the dialer of your phone and start typing a number, you will probably get search results from the save contacts for the number you entered. Your task is to implement a similar feature.
Saved contacts are numbered from 0 to N-1. They are represented by two arrays A,B of N strings each. Name of K-th contact is A[K] and phone number is B[K].
Write a function
class Solution { public String solution(String[] A, String[] B, String P); }
which, given two arrays A and B and a string P of length M representing a partial phone number, returns the contact name whose phone number contains P as a substring, that is a contiguous segment (for example, “436800143” contains as a substring “6800”, but not “3614”).
If there is more than one contact matching the search criteria, your function should return the alphabetically smallest contact name.
If no match is found, your function should return “NO CONTACT”.

Examples:

Given A = [“pim”, “pom”], B = [“999999999”, “777888999”] and P = “88999”, your function should return “pom”, because only pom’s phone number contains “88999”.
Given A = [“sander”, “amy”, “ann”, “michael”], B = [“123456789”, “234567890”, “789123456”, ‘“123123123”’] and P = “1”, your function should return “ann”. Note that sander, ann and michael’s phone number contain “1” but “ann” is alphabetically smaller.
```js
function findcontactList(nameArr, numberArr, searchStr) {
  let contactList = [];
  for (let i = 0; i < nameArr.length; i++) {
    contactList.push({ name: nameArr[i], phoneNumber: numberArr[i] });
  }
  return contactList
    .filter((item) => item.phoneNumber.match(searchStr))
    .sort((a, b) => {
      let textA = a.name.toUpperCase();
      let textB = b.name.toUpperCase();
      return textA < textB ? -1 : textA > textB ? 1 : 0;
    })[0].name || "NO CONTACT";
}
```
## Count of different numbers divisible by 3 that can be obtained by changing at most one digit
Given a string str[] number N, the task is to calculate the number of ways to make the given number divisible by 3 by changing at most one digit of the number.
```js
function numbersDivisibleBy3(str) {
  function totalNum(arr) {
    return arr.reduce((prev, current) => Number(prev) + Number(current));
  }
  let listResult = [];
  let strToArray = [...str];
  let strToArrayCopy = [...strToArray];
  for (let i = 0; i < strToArray.length; i++) {
    for (let j = 0; j < 10; j++) {
      if (strToArray[i] !== j) {
        strToArrayCopy[i] = j;
        if (totalNum(strToArrayCopy) % 3 === 0) {
          listResult.push(strToArrayCopy.join(""));
        }
        strToArrayCopy = [...strToArray];
      }
    }
  }
  const uniqueListResult = new Set(listResult.sort());
  return `We have ${
    uniqueListResult.size
  } different numbers divisible by 3 includes : ${[...uniqueListResult]}`;
}
```
