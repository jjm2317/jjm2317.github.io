---
title: ui CarouselSlider
date: 2020-11-19 11:38:27
category: "etc"
draft: false
---
# Slider UI

## 캐러셀  슬라이더 ui

- 캐러셀 (Carousel)
  - 슬라이드 형태의 컨텐츠를 순환하며 표시하는 ui





- 슬라이드 이동
  - 캐러셀 요소를 고정한 상태에서 슬라이더들의 컨테이너인 carousel-item-container 요소를 이동시키면 슬라이더가 이동하는 것처럼 보인다. carousel-item-container 요소를 왼쪽으로 이동시키면 이전 슬라이더로 이동하고 carousel-item-container 요소를 오른쪽으로 이동시키면 다음 슬라이더로 이동한다. 이때 carousel-item-container요소의 이동거리는 슬라이더 하나의 width 와 같다. 
- 무한루핑 기능
  - 슬라이더의 선두에 마지막 슬라이더, 마지막에 첫번째 슬라이더를 클론하여 추가
  - 클론하여 슬라이더의 선두에 추가한 마지막 슬라이더로 이동하면 더이상 이전 슬라이더로 이동할 수 없다. 따라서 뒤쪽에 존재하는 동일한 슬라이더로 이동한다.

### Carousel 의 window

```css
.carousel {
    position: relative;
    margin: 0 auto;
    overflow: hidden;
   	
    border: 1px solid #000;
    
    opacity: 0;
}
.carousel-item-container{
    display: flex;
}

.carousel-item {
    padding: 5px;
}
.carousel-item img{
    vertical-align: bottom
}
/*prev next 버튼*/
.carousel-control{
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    font-size: 2em;
    color: #fff;
    background-color: transparent;
    border-color: transparent;
    cursor: pointer;
    z-index: 99;
}

.carousel-control:focus{
    outline:none;
}

.carousel-control.prev {
    left: 0;
}

.carousel-control.next{
    right: 0;
}

.carousel-control.disabled{
    opacity: 0.5;
}

.carousel {
    overflow: visible;
}

#overflow:checked + .carousel {
    overflow:hidden;
}
```

**javascript**

```javascript
class Carousel {
	constructor() {
		this.carousel = document.querySelector('.carousel');
        this.container = this.carousel.querySelector('.carousel-item-container');
        this.item = this.carousel.querySelector('.carousel-item');
        
        this.prev = this.carousel.querySelector('.prev');
        this.next = this.carousel.querySelector('.next');
        
        this.itemWidth = this.item.offsetWidth;
        
        this.itemHeight = this.item.offsetHeight;
        
        this.itemLength = this.carousel.querySelectorAll('.carousel-item').length;
        
        this.offset = 0;
        
        this.currentItem = 1;
        this.config = {
            duration: 200,
            easing:'ease-out';
        };
        this.init();
        this.attachEvent();
	}
    
    init() {
        this.carousel.style.width = this.item.itemWidth + 'px';
        this.carousel.style.heigth = this.item.itemHeight + 'px';
        this.carousel.style.opacity = 1;
        
        this.checkMovable();
    }
    attachEvent() {
        this.prev.addEventListener('click', this.moveToPrev.bind(this));
        this.next.addEventListener('click', this.moveToNext.bind(this));
    }
    
    moveToPrev() {
        this.offset += this.itemWidth;
        
        this.move();
        
        this.currentItem--;
        this.checkMovable();
        
        
    }
    moveToNext() {
            this.offset -= this.itemWidth;
            
            this.move();
            this.currentItem++;
            this.checkMovable();
    }
    move() {
        this.container.style.transition = `transform${this.config.duration}ms ${this.config.easing}`;
        this.container.style.transform  `translate#D(${this.offset}px, 0, 0)`;
    }
    checkMovable() {
        if(this.currentItem === 1){
            this.prev.disabled = true;
            this.prev.classList.add('disabled');
        } else{
            this.prev.disabled = false;
            this.prev.classList.remove('disabled');
        }
        
        if(this.currentItem === this.itemLength) {
            this.next.disabled = true;
            this.next.classList.add('disabled');
        } else{
            this.next.disabled = false;
            this.next.classList.remove('disabled');
        }
    }
    
}
window.onload = function () {
        const carousel = new Carousel();
}
```

