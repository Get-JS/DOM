## Window의 주요 프로퍼티와 메서드

## 1. Window

- **`Window 객체는`** 
  - 전역 객체이며, 
  - 전역 변수는 Window 객체의 프로퍼티 이다. 
- Window 객체의 프로퍼티와 메서드는 **window 프로퍼티로 참조할 수 있다.**

### Window 객체의 주요 프로퍼티

property | 의미
---|---|
`screen`                              | Screen 객체를 가리킨다. 
`document`                            | Document 객체를 가리킨다.    
`location`                            | Location 객체를 가리킨다. 
`navigator`                           | Navigatory 객체를 가리킨다. 
`hitory`                              | History 객체를 가리킨다. 
`event`                               | Event 객체를 가리킨다. 
`console`                             | Console 객체를 가리킨다. 
`window`                              | Window 객체를 가리킨다. 
`self`                                | Window 객체를 가리킨다.(window 프로퍼티와 같음) 
`parent`                              | 해당 창이 프레임 안의 창이면 부모 window 객체를 가리킨다. 그렇지 않으면 자기 자신을 가리킨다.
`top`                                 | 해당 창이 프레임 안의 창이면 top 레벨의 window 객체를 가리킨다. 그렇지 않으면 자지 자신을 가리킨다.
`opener`                              | 현재 창을 생성한 창을 가리킨다. 
`frames[]`                            | 창에 포함된 각 프레임을 가리키는 참조가 저장된 배열  
`closed`                              | 현재 창이 닫혀 있는지를 뜻하는 논리값
`name`                                | 현재 창의 이름(읽기/쓰기 가능)
`status`                              | 상태 표시줄의 텍스트(읽기/쓰기 가능)
`screenX, scrrenY`                    | 컴퓨터 화면의 왼쪽 부분을 기준으로 했을 때 브라우저의 왼쪽 위 꼭짓점의 수평 위치와 수직 위치, IE는 지원 하지 않는다. 
`screenLeft, scrrenTop`               | 각각 screenX, screenY와 같다. 파이어폭스는 지원하지 않는다.   
`innerHeight, innerWidth`             | 창 안쪽의 높이와 너비(스크롤 막대가 차지하는 영역은 제외함)
`outerHeight, outerWidth`             | 창 바깥의 높이와 너비(스크롤 막대가 차지하는 영역을 포함)
`scrollX, scrollY`                    | 수평 방향과 수직 방향으로 HTML 문서가 스크롤되는 픽셀의 수
`pageXOffset, pageYOffset`            | 각각 scrollX, scrollY와 같다.

### Window 객체의 주요 메서드

property | 의미
---|---|
`alert(message)`                              | 경고 대화상자를 표시한다.
`promt(message,defalut)`                      | 입력 대화상자를 표시한다.
`confirm(question)`                           | 확인 대화상자를 표시한다.
`setTimeout(callback,interval)`               | interval(ms)이다. callback을 호출 한다. 
`setInterval(callback,delay)`                 | delay(ms) 후에, callback을 호출 한다.
`clearTimeout(timeoutId)`                     | timeoutId의 setTimeout을 취소한다.
`clearInteval(intervalId)`                    | intervalId의 setInterval을 취소한다.
`blur()`                                      | 창에서 포커스를 제거한다.
`focus()`                                     | 창에 포커스를 준다.
`close()`                                     | 창을 닫는다.
`open()`                                      | 새로운 창을 연다.
`moveBy(x,y)`                                 | 창을 수평으로 x, 수직으로 y만큼 이동한다.
`moveTo(x,y)`                                 | 창을 좌표(x,y)로 이동한다.
`resizeBy(width, hegith)`                     | 창의 너비를 width, 높이를 heigth만큼 키운다.
`resizeTo(width, height)`                     | 창의 너비를 width, 높이를 hegith로 설정한다.
`scrollBy(x,y)`                               | 스크롤을 수평으로 x, 수직으로 y만큼 이동한다.
`scrollTo(x,y)`                               | 스크롤을 좌표(x, y)로 이동한다.
`print()`                                     | 창 안에서 문서를 인쇄하는 대화상자를 연다.

## 2. Location

- **`Location 객체는`** 
  - 창에 표시되는 문서의 URL을 관리한다.
- Location 객체는 window.location 또는 location으로 참조 가능하다.

### Location 객체의 프로퍼티

property | 의미 | 예
---|---|---|
`hash`                        | 앵커 부분 | #achor
`host`                        | 호스트 이름:포트번호 | www.example.com:80
`hostname`                    | 호스트 이름 | www.example.com
`href`                        | 전체 URL | http://www.example.com:80/test/index.html?q=value#achor
`pathname`                    | 웹 사이트의 루트를 기준으로 한 상대 경로 | /test
`port`                        | 포트 번호 | 80
`protocol`                    | 프로토몰 | http:
`search`                      | 질의 문자열 | ?q=value

###  Location 객체의 메서드

property | 의미
---|---|
`assign(url)`                        | url이 가리키는 문서를 읽는다.
`reload()`                           | 문서를 다시 읽어 들인다.
`replace(url)`                       | url로 이동한다. 웹 브라우저의 이력에 남지 않는다.
`toString()`                         | location.href 값을 반환한다.

#### URI(Uniform Resource Identifier) 인코딩

```js
    encodeURI() // 영문, 숫자, 예약문자(;,/,?,:,@,&,=,+,$), 이스케이프 하지 않은 기호(-,_,!,~,*,(,),')는 인코딩을 하지 않는다.
    encodeURIComponent() // 영문, 숫자, 예약문자(;,/,?,:,@,&,=,+,$), 이스케이프 하지 않은 기호(-,_,!,~,*,(,),')까지 인코딩 한다.
    decodeURI()
    decodeURIComponent()
```
## 3. History 

- **`History 객체는`**
  - 창의 웹 페이지 **열람 이력을 관리한다.**
- History 객체는 window.history 또는 history로 참조 가능하다.

### History 객체의 프로퍼티 

property | 의미
---|---|
`length`                        | 현재 세션의 이력 개수(읽기 전용)
`scrollRestoration`             | 웹 페이즈를 이동한후에 동작하는 웹 브라우저의 자동 스크롤 기능을 켜거나 끄는 값. "auto" 또는 "manual"이 들어갈 수 있다.
`state`                         | pushState와 replaceState 메서드로 설정한 state 값(읽기 전용)

### History 객체의 메서드

property | 의미
---|---|
`back()`                                | 창의 웹 페이지 열람 이력을 하나 되돌린다.
`forward()`                             | 창의 웹 페이지 열람 이력을 하나 진행한다.
`go(number)`                            | 창의 웹 페이지 열람 이력을 number만큼 진행한다. number 값이 음수면 그 만큼 되돌린다.
`pushState(state,title,url)`            | 창에 웹 페이지 열람 이력을 추가한다. 페이지는 이동하지 않는다.
`replaceState(state,title,url)`         | 현재 창의 열람 이력을 수정한다.

## 4. Navigator

- **`Navigator 객체는`**
  - 스크립트가 실행중인 웹 브라우저 등의 애플리케이션 정보를 관리한다.
- Navigator 객체는 window.navigator 또는 navigator로 참조할 수 있다.

### Navigator 객체의 주요 프로퍼티

property | 의미
---|---|
`appCodeName`         | 웹 브라우저의 내부 코드 네임. (정확하지 않음) 
`appName`             | 웹 브라우저 이름 (정확하지 않음)
`appVersion`          | 웹 브라우저 버전 (정확하지 않음)
`gelocation`          | 단말기의 물리적 위치를 관리하는 Geoloaction 객체
`language`            | 웹 브라우저의 UI언어("en","en-US","ko","ko-KR","fr".. etc)
`mimeTypes[]`         | 웹 브라우저가 지원하는 MIME 타입 목록을 저장한 MimeTypeArray 객체
`onLine`              | 웹 브라우저가 네트워크에 연결되어 있는지를 뜻하는 논리값
`platform`            | 웹 브라우저의 플랫폼, 윈도우 "win32",맥은 "MacIntel"
`plugins`             | 웹 브라우저에서 설치된 플러그인 목록을 가리키는 Plugin 객체의 배열
`userAgent`           | 웹 브라우저가 USER-AGET 헤더에 보내는 문자열

### Navigator 객체의 주요 메서드

property | 의미
---|---|
`javaEnabled()`                                        | Java를 사용할 수 있는지를 뜻하는 논리값을 반환 
`getUserMedia()`                                       | 단말기의 마이크와 카메라에서 audio와 video 스트림을 반환
`resgisterContentHandler(mimeType,uri,title)`          | 웹 사이트를 특정 MIME 타입과 연결
`vibrate()`                                            | 단말기를 진동시킴

## 5. Screen

- **`Screen 객체는`** 
  - 화면(모니터) 크기와 색상 등의 정보를 관리한다. 
- Screen 객체는 window.screen 또는 screen로 참조할 수 있다.

### Screen 객체의 주요 프로퍼티

property | 의미
---|---|
`availTop`             | 사용할 수 있는 화면의 첫 번째 픽셀의 y좌표
`availLeft`            | 사용할 수 있는 화면의 첫 번째 픽셀의 x좌표
`availHeight`          | 사용할 수 있는 화면의 높이
`availWidth`           | 사용할 수 있는 화면의 너비
`colorDepth`           | 웹화면의 색상 심도(비트 수) 약 1,678만 색상이면 24
`pixelDepth`           | 화면의 비트 심도(비트 수) 약 1,678만 색상이면 24(IE9는 제공하지 않음)
`height`               | 화면 높이
`width`                | 화면 너비
`orientation`          | 화면 방향

## 6. Document

### Document 객체의 주요 프로퍼티

property | 의미
---|---|
`charcterSet`             | 문서에 적용된 문자 인코딩(읽기 전용)
`cookie`                  | 문서의 cookies를 쉼표로 연결한 문자열
`domain`                  | 문소서의 도메인(읽기 전용)
`lastModified`            | 문서를 마지막 수정한 날(읽기 전용)
`location`                | window.location 프로퍼티와 마찬가지로 Location 객체를 가리킴
`readyState`              | 문서를 읽어 들인 상태(읽기 전용)
`referrer`                | 문서에 링크된 페이지 URL(읽기 전용)
`title`                   | 문서 제목
`URL`                     | 문서 URL(읽기 전용)

### Document 객체의 주요 메서드

property | 의미
---|---|
`close()`                   | document.open() 메서드로 연 문서를 닫는다.
`open()`                    | 문서를 쓰기 위해 연다.
`write(text)`               | document.open() 메서드로 연 문서에 기록한다.
`writeln(text)`             | document.open() 메서드로 연 문서에 기록하고 개행 문자를 추가한다.