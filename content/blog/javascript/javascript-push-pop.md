---
title: javascript push&pop
date: 2020-10-19 15:08:23
category: "javascript"
draft: false
---

# javascript push, pop

## push & pop

```
Array.prototype.myPush = function( ...args) {
  for(let i = 0; i< args.length; i++){
    this[this.length] = args[i];
  }
  return this.length;
}

Array.prototype.myPop = function() {
  let res;
  res = this[this.length-1];
  this.length = this.length - 1;

  return res;
}
const a = [1, 2, 3]

console.log(a.myPush(3,4));
console.log(a);
console.log(a.myPop());
console.log(a);

/*
5
[ 1, 2, 3, 3, 4 ]
4
[ 1, 2, 3, 3 ]
*/
```
