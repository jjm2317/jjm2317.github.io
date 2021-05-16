---
title: javascript SearchPractice
date: 2020-09-18 12:57:42
category: "javascript"
draft: false
---

# 선형 검색 이진검색 과제

```
function linearSearch(array, target){
  for(let i = 0; i < array.length; i ++){
    if(array[i]===target){
      return i;
    }
  }
  return -1;
}

console.log(linearSearch([1,2,3,4,5,6] , 6));

function binarySearch(array, target) {
  let start = 0;
  let end = array.length - 1;
  let mid = parseInt(( start + end ) / 2)

  while (start !== end) {
    if(array[mid] < target ) {
      start = mid + 1;
      mid = parseInt(( start + end ) / 2);
    }else if (array[mid] > target) {
      end = mid - 1;
      mid = parseInt(( start + end ) / 2);
    }

    if(array[mid] === target){
      return mid;
    }
  }
  return -1;
}

console.log(binarySearch([1,2,3,4,5,6],4));
```
