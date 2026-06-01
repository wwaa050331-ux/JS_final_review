# ⭐️자바스크립트 기말고사 범위 정리

---

## 1일차 이벤트 함수(week9)
**부가적인 개념**
### 🔄 두 기능의 차이점 한 눈에 보기

| 메서드 | 역할 | 쉽게 말하면 | 원본 데이터 변경 여부 |
| :--- | :--- | :--- | :--- |
| **`getAttribute()`** | 속성값을 가져옴 | **읽기 (Read / Copy)** | 원본 데이터 유지됨 |
| **`setAttribute()`** | 속성값을 변경/추가함 | **쓰기 (Write / Update)** | 원본 데이터가 바뀜 |

ex) elem.setAttribute("src", img.getAttribute("src"));  

1단계 (오른쪽: Ctrl + C) 👉 img.getAttribute("src")  

img(내가 방금 클릭한 작은 썸네일 이미지)의 src 주소표를 읽어서 복사합니다.  

컴퓨터 머릿속: "어, 지금 클릭한 이미지 주소가 "dog.jpg"네? 기억해야지!"


2단계 (왼쪽: Ctrl + V) 👉 elem.setAttribute("src", ...)  

복사해 온 주소("dog.jpg")를 elem(화면에 떠 있는 큰 메인 이미지)의 src에다가 덮어쓰기(변경) 합니다.
컴퓨터 머릿속: "큰 이미지(elem)야, 네 주소 지우고 방금 복사한 "dog.jpg"로 새로 갈아끼워!"

🛠️ HTML 요소를 잡아오는 집게 5가지

1. document.getElementById("아이디명")
대상: id 속성으로 찾기

2. document.getElementsByClassName("클래스명")
일치하는 것 전부(그룹) 가져옴 
대상: class 속성으로 찾기

3. document.getElementsByTagName("태그명")
일치하는 것 전부(그룹) 가져옴
대상: div, p, img 같은 HTML 태그 이름으로 찾기

4. document.querySelector("선택자")
설명: CSS 선택자로 찾아서 가장 먼저 발견된 딱 1개만 가져옵니다.
클래스는 . 아이디는 #

5. document.querySelectorAll("선택자")
설명: CSS 선택자와 일치하는 것 전부(그룹)를 가져옵니다.

**주요 마우스 이벤트**
1. 키보드
* click
마우스 버튼을 클릭했을 때
* dbclick
마우스 버튼을 더블 클릭했을 때
* mousemove
마우스를 움직일 때 (터치스크린에서 동작하지 않는다)

2. UI
* scroll
사용자가 페이지를 위아래로 스크롤할 때
* select
텍스트를 선택했을 때

3. 폼
* input
input 또는 textarea 요소의 값이 변경되었을 때
contenteditable 어트리뷰트를 가진 요소의 값이 변경되었을 때
* change
select box, checkbox, radio button의 상태가 변경되었을 때
* submit
form을 submit할 때 (버튼 또는 키)
* reset
reset 버튼을 클릭할 때 (최근에는 사용 안함)

**on+eventType**

프로그램이 혼재되는 것을 막아줌
```html
// 1. 할 일들을 다 모아놓은 '세트 메뉴 명령서'를 만듭니다.
function 슈퍼이벤트() {
    춤추기();    // 첫 번째 일
    노래하기();  // 두 번째 일
    불켜기();    // 세 번째 일
}

// 2. onclick에는 이 '세트 메뉴' 딱 하나만 연결합니다.
로봇.onclick = 슈퍼이벤트;
```
**표준 이벤트 모델**  

* addEventListener
EventTarget.addEventListener('eventType','funtionName'[.useCapture]);
다중 핸들러 지원

```html
// 마법 게시판에는 명령을 계속 추가(Add)할 수 있습니다!

로봇.addEventListener('click', 춤추기);   // 1번 명령 부착!
로봇.addEventListener('click', 노래하기); // 2번 명령 또 부착! (안 지워짐)
로봇.addEventListener('click', 불켜기);   // 3번 명령 또 부착! (다 기억함)
```

**이벤트 핸들러 내에서의 this**  

window 객체
이벤트가 있을땐 이벤트를 지정(Event.currentTarge랑 같은 기능)
```html
let 버튼 = document.getElementById("my-btn");

// 고전 방식이나 표준 방식(addEventListener) 모두 동일합니다.
버튼.onclick = function() {
    console.log(this); // ❓ 요정아, 네 주인님 누구니? -> "이 버튼이요!"
}; (currentTarget)
```

**createElement**  

html 안에 공간을 만들어줌
코드 예시)

```html
// 1. p 태그(글자 상자)를 새로 만든다.
let newParagraph = document.createElement("p");

// 2. 상자 안에 글자를 적어 넣는다. (새로 배운 getAttribute 세트 친구!)
newParagraph.innerText = "안녕하세요! 새로 태어난 글자입니다. ✨";

// 3. 글자 색을 빨간색으로 꾸며본다.
newParagraph.style.color = "red";

// 4. 화면(body)에 최종적으로 탕! 탕! 조립해서 붙인다.
document.body.appendChild(newParagraph);
```
**🪂 내려가는 길(캡처링) vs 🎈 올라오는 길(버블링)**
addEventListener 맨 뒤에 붙은 true와 false가 바로 "너 신호가 내려갈 때 반응할래? 올라올 때 반응할래?"를 결정하는 비밀 스위치입니다.  

true (캡처링 스위치): 신호가 목적지로 내려가는 길에 나를 지나가면 즉시 반응해라!  

false (버블링 스위치): 신호가 목적지를 찍고 다시 올라오는 길에 나를 지나가면 반응해라! (아무것도 안 적으면 기본적으로 false가 됩니다.)  
```html
// 1. body 변수 (실제로는 false이므로 '버블링' 때 실행됨!)
body.addEventListener('click', function () { ... }, false);

// 2. p 변수 (true이므로 '캡처링'인 내려갈 때 실행됨!)
para.addEventListener('click', function () { ... }, true);

// 3. button 변수 (true이므로 목적지 단계에서 실행됨!)
button.addEventListener('click', function () { ... }, true);
```
Handler for paragraph.  (내려갈 때 p가 먼저 낚아챔)  

Handler for button.     (목적지 도착)  

Handler for body.       (올라갈 때 body가 마지막에 낚아챔)

