## 문제 🔒
[topKFrequent](https://leetcode.com/problems/top-k-frequent-elements/submissions/)

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

```
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

```
Example 2:
Input: nums = [1], k = 1
Output: [1]
```

## 풀이 🔍

```js
// 배열 중복 요소 개수 - https://hianna.tistory.com/459 참고

var topKFrequent = function(nums, k) {
    const sortNums = nums.reduce((accu,curr)=> {
    accu.set(curr, (accu.get(curr)||0) +1) ;
    return accu;
    },new Map());
    console.log(sortNums);
		// Map(3) { 1 => 3, 2 => 2, 3 => 1 }
    
    let answer  = [];
    for (let [key, value] of sortNums.entries()) {
	    answer.push(key);
    }
      
    return answer.slice(0,k);
};
```
<br><br>

### 오류 원인 📍

sort가 안되어 있었음! 
<br><br>

### 해결 방법 🔑

- sortNums 배열의 이름을 countNums로 변경하고
- sort()를 사용하는 새로운 배열 sortNums를 만들고
- 길이가 k인 반복문 for문을 사용해서 key의 순서대로 answer배열에 key값을 push하기 

(thanks to 이불님💙)

```js
var topKFrequent = function(nums, k) {
    let answer  = [];

    const countNums = nums.reduce((accu,curr)=> {
    accu.set(curr, (accu.get(curr)||0) +1) ;
    return accu;  
    },new Map());
    
		//sort! 
    const sortNums = [...countNums].sort((a,b) =>b[1]-a[1]);
    
    for (let i=0; i<k; i++){
        answer.push(sortNums[i][0]);
    }     
    return answer;
};
```
