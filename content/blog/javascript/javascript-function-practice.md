---
title: javascript function practice
date: 2020-09-18 16:43:03
category: "javascript"
draft: false
---

# 0918 function 과제

## 문제 1. 1 ~ 10,000의 숫자 중 8이 등장하는 횟수 구하기 (Google)

1부터 10,000까지 8이라는 숫자가 총 몇번 나오는가? 이를 구하는 함수를 완성하라.
단, 8이 포함되어 있는 숫자의 갯수를 카운팅 하는 것이 아니라 8이라는 숫자를 모두 카운팅 해야 한다. 예를 들어 8808은 3, 8888은 4로 카운팅 해야 한다.
(hint) 문자열 중 n번째에 있는 문자 : str.charAt(n) or str[n]

```
function getCount8 () {

}
console.log(getCount8()); // 4000
```

**Answer**

```
function getCount8 () {
  let string = '';
  let count = 0;
  for( let i = 1; i <= 10000; i++){
    string += i;
  }
  for( let j = 0; j < string.length; j ++){
    if(string[j] === '8') count++;
  }
  return count;
}
console.log(getCount8());//4000
```

## 문제 2. 이상한 문자 만들기

toWeirdCase함수는 문자열을 인수로 전달받는다. 문자열 s에 각 단어의 짝수번째 인덱스 문자는 대문자로, 홀수번째 인덱스 문자는 소문자로 바꾼 문자열을 리턴하도록 함수를 완성하라.
예를 들어 s가 ‘hello world’라면 첫 번째 단어는 ‘HeLlO’, 두 번째 단어는 ‘WoRlD’로 바꿔 ‘HeLlO WoRlD’를 리턴한다.
주의) 문자열 전체의 짝/홀수 인덱스가 아니라 단어(공백을 기준)별로 짝/홀수 인덱스를 판단한다.

```
function toWeirdCase(s) {}console.log(toWeirdCase('hello world'));    // 'HeLlO WoRlD'
console.log(toWeirdCase('my name is lee')); // 'My NaMe Is LeE'
```

**Answer**

```
function toWeirdCase(s){
  let index = 0;
  let newString = '';
  for (let i = 0; i<s.length; i++){
    let asciiNum = s[i].charCodeAt(0);
    //공백이면 넘어가기
    if (s[i] === ' '){
      newString += ' ';
      index = 0;
      continue;
    }
    //알파벳 아니면 그냥 저장
    if(!((asciiNum >=65 && asciiNum <= 90) || (asciiNum >=97 && asciiNum <= 122))){
      newString += s[i];
      index ++;
      continue;
    }
    if (index % 2 === 0) {
      // 대문자면 그냥 저장, 소문자면 대문자로바꾸기
      if(asciiNum >=65 && asciiNum <= 90){
        newString += s[i];
      }else{
        newString += String.fromCharCode(asciiNum - 32)
      }
      index ++;
    }else{
      //대문자면 소문자로 바꾸기, 소문자면 그냥 저장
      if(asciiNum >=65 && asciiNum <= 90){
        newString += String.fromCharCode(asciiNum + 32)
      }else{
        newString += s[i];
      }
      index ++;
    }
  }
  return newString;
}

console.log(toWeirdCase('ahf@@sk!!dhf fD%%FDFas'));
//AhF@@sK!!dHf Fd%%FdFaS
```
