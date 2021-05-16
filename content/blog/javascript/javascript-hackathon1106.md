---
title: javascript hackathon1106
date: 2020-11-11 08:50:00
category: "javascript"
draft: false
---

# 11/06 해커톤

- 주제
  - 이상형 월드컵
  - 조건에 따라 사진 필터링

**다음부터는**

- 작업 단위마다 데드라인 정하기
- git 사용법 확실히 공부하고 진행
- 기획 더 신경써서 하기

## index.html

```
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Worldcup</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.css">
  <link rel="stylesheet" href="css/style.css">
  <script src="js/data.js"></script>
  <script src="js/app.js" defer></script>
</head>
<body>
  <div class="container">
    <!--랜딩1-->
    <!-- <div class="wrap2">
      <div class="wrap">
    <h1>logo</h1>
    </div>
  </div> -->
    <div class="main">
      <h2>이상형 월드컵</h2>
      <p>너.의.맘.이.궁.금.해</p>
      <div class="gender active">
        <button class="woman">여자</button>
        <button class="man">남자</button>
        <button class="next">NEXT</button>
      </div>
      <div class="job">
        <button class="prev">이전</button>
        <button class="singer">가수</button>
        <button class="actor">배우</button>
        <button class="all">모두</button>
        <button class="start">START</button>
      </div>
      <div class="battle">
        <h3>16강</h3>
        <figure class="left">
          <img src="" alt="leftimg">
          <caption>이름</caption>
        </figure>
        <figure class="right">
          <img src="" alt="rightimg">
          <caption>이름</caption>
        </figure>
      </div>
      <!-- <div class="battle">
        <figure>
          <img src="" alt="">
          <caption>당신의 이상형은 IMGNAME입니다.</caption>
        </figure>
        <button class="retry">Goback</button>
        <button class="rank">랭킹보기</button>
      </div> -->
      <span>FAST</span>
      <span>CAMPUS COUPLE</span>
    </div>
  </div>
</body>
</html>
```

## app.js

```
const $gender = document.querySelector('.gender');
const $job = document.querySelector('.job');
const $next = document.querySelector('.gender > .next')
const $singer = document.querySelector('.singer');
const $start = document.querySelector('.start');
const $battle = document.querySelector('.battle');
const $h3 = document.querySelector('.battle h3');
const $leftImg = document.querySelector('.left > img');
const $rightImg = document.querySelector('.right > img');
//gender 선택 시작
let jobKey = '';
let genderChoice ='';
let NewidealType = [];
let numArr = [];
let count = 0;
let check = [];
let match8Index = [];
let match4Index = [];
let match2Index = [];
let match1Index = [];
let match8 = [];
let match4 = [];
let match2 = [];
let match1 = [];
let tournament =[]
function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min; //최댓값은 제외, 최솟값은 포함
}
const ranDom = n => {
  while (!(numArr.length === n)){
    while (1){
      let num = getRandomInt(0, n)
      if(!numArr.includes(num)){
       numArr.push(num);
       break;
      }
    }
  }
}
//gender 선택 이벤트 핸들러 등록
$gender.onclick = e => {
  if(e.target.matches('.gender > next')) return;
  if(e.target.matches ('.gender > .woman')){
    genderChoice = 'w'
  }
  else if(e.target.matches('.gender > .man')){
    genderChoice = 'm'
  } else return;
}
//gender 선택 끝
// next 버튼을 누르면 gender에 active 삭제, job에 active 추가하는 이벤트 핸들러
$next.onclick = e => {
  if ( !genderChoice ) {
    alert('성별을 선택하세요!');
    return;
  };
  e.target.parentNode.classList.remove('active');
  $job.classList.add('active');
  console.log($job);
}
$job.onclick = e => {
  if (e.target.matches('.job > .prev')) {
    $job.classList.remove('active');
    $gender.classList.add('active');
    jobKey = '';
    genderChoice = '';
  } else if (e.target.matches('.job > .singer')){
    jobkey = 'singer'
  } else if (e.target.matches('.job > .actor')) {
    jobkey = 'actor'
  } else if(e.target.matches('.job > .all')){
    jobkey = 'all'
  } else return;
  console.log(jobkey);
}
$start.onclick = () => {
   NewidealType = idealType.filter(ideal => {
    return jobkey==='all' ? ideal.gender === genderChoice :
    ideal.gender === genderChoice && ideal.job === jobkey
  });
  if (jobkey === 'all' ) {
    ranDom(32);
    numArr.length = 16;
    randomItem(NewidealType);
    NewidealType.length = 16;
  }
  $job.classList.remove('active');
  $battle.classList.add('active');
  tournament = matchImage(NewidealType);
  renderImage(tournament,0);
 }
 const randomItem = () => {
  NewidealType = NewidealType.map((item, i, arr) => arr[numArr[i]]);
  }
  const matchImage = (match) => {
    const res = match.map(item => {
      console.log(item);
      return item.path});
    console.log(res);
    return res;
  }
const renderImage = (pathSet, n) => {
  console.log(pathSet[2*n]);
  $leftImg.setAttribute('src', pathSet[2*n]);
  $rightImg.setAttribute('src', pathSet[2*n+1]);
}
$battle.onclick = e => {
  count = count + 1;
  // if (e.target === $leftImg) {
  //   NewidealType[0].lank = 1;
  // } else {
  //   NewidealType[0].lank = 1;
  // }
  console.log(count);
  console.log(tournament)
  if(count < 8){
    renderImage(tournament,count);
    if(e.target.parentNode.matches('.left')){
      match8Index.push(2*count);
    }else{
      match8Index.push(2*count+1);
    }
  }
  if(count >=8 && count<12) {
    renderImage(tournament,count-8);
    if(e.target.parentNode.matches('.left')){
      match4Index.push(2*(count-8));
    }else{
      match4Index.push(2*(count-8)+1);
    }
  }
  if(count >=12 && count<14){
    renderImage(tournament,count-12);
    if(e.target.parentNode.matches('.left')){
      match2Index.push(2*(count-12));
    }else{
      match2Index.push(2*(count-12)+1);
    }
  }
  if(count === 14){
    renderImage(tournament,count-14);
    if(e.target.parentNode.matches('.left')){
      match1Index.push(2*(count - 14));
    }else{
      match1Index.push(2*(count-14)+1);
    }
  }
  if (count === 8) {
    $h3.textContent = '8강';
  } else if(count === 12) {
    $h3.textContent = '4강';
  } else if(count === 14){
    $h3.textContent = '결승'
  } else if(count === 15){
    $h3.textContent = ''
  }
  if(count===8){
    match8 = NewidealType.filter((_,i) => match8Index.includes(i))
    console.log(match8);
    tournament= matchImage(match8);
  };
  if(count===12){
    match4 = match8.filter((_,i) => match4Index.includes(i))
    console.log(match4);
    tournament=matchImage(match4);
  };
  if(count===14){match2 = match4.filter((_,i) => match2Index.includes(i));
    console.log(match2);
    tournament = matchImage(match2);
  }
  if(count===15){match1 = match2.filter((_,i) => match1Index.includes(i));
    console.log(match1);
    tournament = matchImage(match1);
    e.target.classList.add('champion');
  }
}
if (count === 15) {
  renderImage(tournament, count -15);
}
// const matchImage = match => {
//   let res = match.map(item => item.path);
//   return res;
//   console.log(NewidealType)
// }
// const renderImage = (pathset, n) => {
//   $leftImg.setAttribute('src', pathset[2*n]);
//   $rightImg.setAttribute('src', pathset[2*n+1]);
// }
```

## style.css

```
.container {
  width: 1100px;
  height:800px;
  position: relative;
  background-color: #fff;
  /* border:1px solid red; */
  margin: 0 auto;
  box-sizing:border-box ;
}
button{
  background-color: #ddd;
  border:none
}
.main {
  width: 550px;
  height:100%;
  margin: 0 auto;
  border:1px solid red;
  text-align: center;
  position:relative;
}
.header{
  width:100%;
  height:150px;
  /* background-color: royalblue; */
  position: relative;
}
.header h2, p {
  text-align: center;
  font-size: 30px;
  font-weight: 800;
}
.header p{
  width:100%;
  padding-top:30px;
  color:#ddd;
}
.header h2{
  width:100%;
  position: absolute;
  top:70px;
  font-size: 40px;
}
.gender,
.job,
.battle {
  width: 550px;
  margin: 0 auto;
}
/* render 1 */
.gender {
  display: none;
  /* background-color: tomato; */
}
.gender.active, .job.active {
  display: block;
}
.battle.active {
  display: flex;
}
.woman,
.man,
.singer,
.actor,
.all {
  width: 500px;
  height: 100px;
  margin: 0 auto;
  display: block;
  margin-bottom: 30px;
  font-size:30px;
  font-weight: 700;
}
.woman:focus,
.man:focus,
.singer:focus,
.actor:focus,
.all:focus{
  color:purple
}
/* .wrap2 */
.wrap {
  display: flex;
  justify-content: center;
  align-items: center;
  width:100%;
  height:800px;
  position: absolute;
  left: 0;
  right: 0;
  z-index: 1;
  overflow: hidden;
  box-sizing: border-box;
}
.wrap {
  background-color: #eee;
}
.wrap > h1 {
  width: 250px;
  height:200px;
  background: url(/img/logo.png) no-repeat;
  background-size: contain;
  text-indent:-9999px;
  text-overflow: ellipsis;
  transform: translateY(-50%);
}
.wrap span{
  font-size: 30px;
  position: absolute;
  margin-left: -20px;
  bottom:calc(50% - 50px);
}
.wrap span:nth-child(4){
  bottom:calc(50% - 100px);
}
.loading {
  animation-duration: 2s;
  animation-name: load;
  animation-fill-mode: forwards;
}
@keyframes load{
  0% {
  transform: translate3d(0);
  }
  100% {
    transform: translate3d(0, -100%, 0);
  }
}
/* 랜딩2 */
  .job {
    margin:20px auto;
    display: none;
    background-color: #bbb;
  }
  .job::after{
    content:'';
    display: block;
    clear: both;
  }
.job > .prev {
  width:60px;
  height:60px;
  position: absolute;
  top:47%;
  left: -100px;
  overflow: hidden;
  text-indent: -9999px;
  background:url(/img/prev.png) no-repeat;
  background-size: contain;
}
.container  h2{
  margin-bottom:30px ;
  font-size: 30px;
}
.container p {
  margin-bottom: 30px;
}
.next {
  width: 150px;
  height: 80px;
  font-size: 50px;
}
.start {
  width: 150px;
  height: 80px;
  font-size: 40px;
}
/* 랜딩 3 */
.battle {
  display: none;
  margin-top: 30px;
}
.main:nth-child(3) h2 {
  color: #abd5bd;
  margin-bottom: 10px;
}
.main:nth-child(3) .battle h3 {
  position: absolute;
  top: 75px;
  left: 155px;
  color: white;
}
.main:nth-child(3) .left {
  display: flex;
  width: 50%;
  height: 200px;
  text-align: center;
  border: 2px solid;
}
.main:nth-child(3) .right {
  display: flex;
  width: 50%;
  height: 200px;
  text-align: center;
  border: 2px solid;
}
/* 랜딩 4*/
/* 랜딩 4*/
.main:nth-child(4) {
}
.battle {
  height: 500px;
  display: none;
  justify-content: center;
  align-items: center;
}
.battle h3 {
  position: absolute;
  top: 150px;
  color: #000;
  font-size: 35px;
  font-weight: 800;
}
.battle figure{
  width : 100%;
  height: 200px;
}
.battle figure img{
  display: block;
  width: 100%;
  height: 300px;
  background-color: green;
}
footer > span {
  left:50%;
  font-size: 20px;
  font-weight: 700;
  /* display: inline-block; */
  /* background-color: royalblue; */
  transform: translateX(-50%);
  position: absolute;
  bottom:100px;
}
footer >span:nth-child(2) {
  bottom:50px;
}
.battleFinal {
  display: none;
}
.champion {
  position: absolute;
  width: 100%;
  transform: scale(2) ;
}
```

- data.js (lank 오타ㅎㅎ.. lank => rank)

```
const idealType = [
  { id: 1, job: 'singer', content: '김동현' , path: '../남자아이돌/김동현.jpg', gender: 'm' ,lank: 0},
  { id: 2, job: 'singer', content: '김상균' , path: '../남자아이돌/김상균.jpg', gender: 'm' ,lank: 0},
  { id: 3, job: 'singer', content: '김지범' , path: '../남자아이돌/김지범.jpg', gender: 'm' ,lank: 0},
  { id: 4, job: 'singer', content: '김태영' , path: '../남자아이돌/김태영.jpg', gender: 'm' ,lank: 0},
  { id: 5, job: 'singer', content: '대준' , path: '../남자아이돌/대준.jpg', gender: 'm' ,lank: 0},
  { id: 6, job: 'singer', content: '성민' , path: '../남자아이돌/성민.jpg', gender: 'm' ,lank: 0},
  { id: 7, job: 'singer', content: '슬로우모션' , path: '../남자아이돌/슬로우모션.jpg', gender: 'm' ,lank: 0},
  { id: 8, job: 'singer', content: '웨비' , path: '../남자아이돌/웨비.jpg', gender: 'm' ,lank: 0},
  { id: 9, job: 'singer', content: '이태용' , path: '../남자아이돌/이태용.jpg', gender: 'm' ,lank: 0},
  { id: 10,job: 'singer',  content: '재범' , path: '../남자아이돌/재범.jpg', gender: 'm' ,lank: 0},
  { id: 11,job: 'singer',  content: '정국' , path: '../남자아이돌/정국.jpg', gender: 'm' ,lank: 0},
  { id: 12,job: 'singer',  content: '제이홉' , path: '../남자아이돌/제이홉.jpg', gender: 'm' ,lank: 0},
  { id: 13,job: 'singer',  content: '최수빈' , path: '../남자아이돌/최수빈.jpg', gender: 'm' ,lank: 0},
  { id: 14,job: 'singer',  content: '포맨' , path: '../남자아이돌/포맨.jpg', gender: 'm' ,lank: 0},
  { id: 15,job: 'singer',  content: '포틴' , path: '../남자아이돌/포틴.jpg', gender: 'm' ,lank: 0},
  { id: 16,job: 'singer',  content: 'boy' , path: '../남자아이돌/boy.jpg', gender: 'm' ,lank: 0},
  { id: 17,job: 'singer',  content: '나연' , path: '../여자아이돌/나연.jpg', gender: 'w' ,lank: 0},
  { id: 18,job: 'singer',  content: '사나' , path: '../여자아이돌/사나.jpg', gender: 'w' ,lank: 0},
  { id: 19,job: 'singer',  content: '레이디' , path: '../여자아이돌/레이디.jpg', gender: 'w' ,lank: 0},
  { id: 20,job: 'singer',  content: '리아' , path: '../여자아이돌/리아.jpg', gender: 'w' ,lank: 0},
  { id: 21,job: 'singer',  content: '무궁화소녀' , path: '../여자아이돌/무궁화소녀.jpg', gender: 'w' ,lank: 0},
  { id: 22,job: 'singer',  content: '산다라박' , path: '../여자아이돌/산다라박.jpg', gender: 'w' ,lank: 0},
  { id: 23,job: 'singer',  content: '설현' , path: '../여자아이돌/설현.jpg', gender: 'w' ,lank: 0},
  { id: 24,job: 'singer',  content: '슬기' , path: '../여자아이돌/슬기.jpg', gender: 'w' ,lank: 0},
  { id: 25,job: 'singer',  content: '신예은' , path: '../여자아이돌/신예은.jpg', gender: 'w' ,lank: 0},
  { id: 26,job: 'singer',  content: '윤하' , path: '../여자아이돌/윤하.jpg', gender: 'w' ,lank: 0},
  { id: 27,job: 'singer',  content: '선미' , path: '../여자아이돌/선미.jpg', gender: 'w' ,lank: 0},
  { id: 28,job: 'singer',  content: '장원영' , path: '../여자아이돌/장원영.jpg', gender: 'w' ,lank: 0},
  { id: 29,job: 'singer',  content: '제니' , path: '../여자아이돌/제니.jpg', gender: 'w' ,lank: 0},
  { id: 30,job: 'singer',  content: '존예진' , path: '../여자아이돌/존예진.jpg', gender: 'w' ,lank: 0},
  { id: 31,job: 'singer',  content: '펀치' , path: '../여자아이돌/펀치.jpg', gender: 'w' ,lank: 0},
  { id: 32,job: 'singer',  content: '지효' , path: '../여자아이돌/지효.jpg', gender: 'w' ,lank: 0},
  { id: 33, job: 'actor', content: '강동원', path: '../남자배우/강동원.jpg', gender: 'm', lank: 0 },
  { id: 34, job: 'actor', content: '강하늘', path: '../남자배우/강하늘.jpg', gender: 'm', lank: 0 },
  { id: 35, job: 'actor', content: '김수현', path: '../남자배우/김수현.jpeg', gender: 'm', lank: 0 },
  { id: 36, job: 'actor', content: '김우빈', path: '../남자배우/김우빈.jpg', gender: 'm', lank: 0 },
  { id: 37, job: 'actor', content: '류준열', path: '../남자배우/류준열.jpeg', gender: 'm', lank: 0 },
  { id: 38, job: 'actor', content: '박보검', path: '../남자배우/박보검.jpg', gender: 'm', lank: 0 },
  { id: 39, job: 'actor', content: '박해일', path: '../남자배우/박해일.jpg', gender: 'm', lank: 0 },
  { id: 40, job: 'actor', content: '소지섭', path: '../남자배우/소지섭.jpg', gender: 'm', lank: 0 },
  { id: 41, job: 'actor', content: '원빈', path: '../남자배우/원빈.jpg', gender: 'm', lank: 0 },
  { id: 42, job: 'actor', content: '유승호', path: '../남자배우/유승호.jpg', gender: 'm', lank: 0 },
  { id: 43, job: 'actor', content: '이민호', path: '../남자배우/이민호.jpg', gender: 'm', lank: 0 },
  { id: 44, job: 'actor', content: '이병헌', path: '../남자배우/이병헌.jpg', gender: 'm', lank: 0 },
  { id: 45, job: 'actor', content: '장기용', path: '../남자배우/장기용.jpg', gender: 'm', lank: 0 },
  { id: 46, job: 'actor', content: '정해인', path: '../남자배우/정해인.jpg', gender: 'm', lank: 0 },
  { id: 47, job: 'actor', content: '지창욱', path: '../남자배우/지창욱.jpg', gender: 'm', lank: 0 },
  { id: 48, job: 'actor', content: '하정우', path: '../남자배우/하정우.jpg', gender: 'm', lank: 0 },
  { id: 49, job: 'actor', content: '공효진', path: '../여자배우/공효진.jpeg', gender: 'w', lank: 0 },
  { id: 50, job: 'actor', content: '권나라', path: '../여자배우/권나라.jpeg', gender: 'w', lank: 0 },
  { id: 51, job: 'actor', content: '김고은', path: '../여자배우/김고은.jpeg', gender: 'w', lank: 0 },
  { id: 52, job: 'actor', content: '김다미', path: '../여자배우/김다미.jpg', gender: 'w', lank: 0 },
  { id: 53, job: 'actor', content: '김태리', path: '../여자배우/김태리.jpeg', gender: 'w', lank: 0 },
  { id: 54, job: 'actor', content: '문채원', path: '../여자배우/문채원.jpeg', gender: 'w', lank: 0 },
  { id: 55, job: 'actor', content: '박민영', path: '../여자배우/박민영.jpeg', gender: 'w', lank: 0 },
  { id: 56, job: 'actor', content: '박소담', path: '../여자배우/박소담.jpg', gender: 'w', lank: 0 },
  { id: 57, job: 'actor', content: '박신혜', path: '../여자배우/박신혜.jpeg', gender: 'w', lank: 0 },
  { id: 58, job: 'actor', content: '박은빈', path: '../여자배우/박은빈.jpeg', gender: 'w', lank: 0 },
  { id: 59, job: 'actor', content: '서예진', path: '../여자배우/서예진.jpg', gender: 'w', lank: 0 },
  { id: 60, job: 'actor', content: '서현진', path: '../여자배우/서현진.jpeg', gender: 'w', lank: 0 },
  { id: 61, job: 'actor', content: '소희', path: '../여자배우/소희.jpeg', gender: 'w', lank: 0 },
  { id: 62, job: 'actor', content: '손예찐', path: '../여자배우/손예찐.jpeg', gender: 'w', lank: 0 },
  { id: 63, job: 'actor', content: '송하윤', path: '../여자배우/송하윤.jpeg', gender: 'w', lank: 0 },
  { id: 64, job: 'actor', content: '정소민', path: '../여자배우/정소민.jpeg', gender: 'w', lank: 0 },
]
```
