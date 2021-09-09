# Javascript_note
Note some helpful piece of code in javascript.
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
