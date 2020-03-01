# 문서 제어

## 1. DOM Tree

- `웹 페이지의 내용은` **Document 객체가 관리한다.**
- 웹 브라우저가 `웹 페이지를 읽어 들이면` **`렌더링 엔진은`** 웹 패이지의 `HTML 문서 구문을 해석하고` `Document 객체에서` 문서 내용을 관리하는 `DOM 트리라고 하는 객체의` **트리 구조를 만든다.**
- 웹 브라우저가 HTML 문서를 읽어 들이면 **`Document 객체로 시작하는 DOM 트리가 만들어진다.`**
- DOM 트리를 구성하는 객체 하나를 노드(Node)라고 한다. 
    - Document 노드: 전체 Document(문서)를 가리키는 `Document 객체`, `document로` **참조 할 수 있다.**
    - HTML 요소 노드: `HTML 요소를` 가리키는 객체
    - 텍스트 노드: `텍스트를` 가리키는 객체
    - 주석 노드
    - 속성 노드

### 1-1. 공백노드

- **HTML은** `요소 뒤에 공백 문자`(공백 문자, 탭 문자, 줄 바꿈 문자 등)가 여러 개 있어도 **무시 한다.**
- 그러나 **DOM 트리는** `요소 앞 뒤에서 연속적인 공백 문자를` 발견하면 `텍스트로 취급하여` 텍스트 노드로 생성한다.
- 이렇게 공백 문자만으로 구성된 텍스트 노드를 **공백노드라고 한다.**
  - 단, **요소(\<html>) 안에** 있는 `첫 공백 문자와 마지막 공백 문자에 대해서는` 공백 노드를 **생성하지 않는다.**

### 1-2. 요소 관계

- `DOM 트리는` HTML 문서 안의 **요소와 텍스트 사이의 포함 관계를 표현 한다.**
- 이 포함 관계는 **부모-자식 관계**라고 부르기도 한다.
- 노드 A 바로 아래에 노드 B가 있을 때, A를 B의 **부모노드**, B를 A의 **자식 노드라고** 한다.
- 같은 부모를 가진 같은 레벨의 노드를 **형제 노드라고** 한다.
- 또한 그 노드가 포함한 노드는 그 노드의 **자식 노드라고**, 그 노드를 포함한 노드는 **조상 노드라고** 한다. 
- `Document 객체는` **모든 노드의 조상 노드이며** **DOM트리의 루트** 이다.

### 1-3. 노드 객체의 프로퍼티

- **`JS를 사용하면`**
  - `DOM 트리의 노드 객체를` 가져와서 제어할 수 있다.
  - `스타일 규칙을` 가져와서 제어할 수도 있다. 
- **`렌더링 엔진은`** DOM트리와 스타일 `규칙이 바뀔 때마다` `트리를 다시 구성해서 웹 페이지를 다시 그린다.`
  - 웹 페이지를 사용자가 조작하거나 JS로 DOM 트리나 스타일을 수정하면 렌더링 엔진은 그때마다 **화면을 다시 렌더링 한다.**
  - 렌더 트리를 다시 구성하고 다시 렌더링하는 처리는 일반적으로 **시간이 많이 걸리는 작업이다.**
- 따라서 이러한 처리가 자주 발생하면 **`렌더링이 원활하지 않을 가능성이 있다.`**
  - 웹 브라우저는 이러한 상황을 피하기 위해 `렌더링 처리 횟수를 가능한 줄이는` **최적화 처리를 한다.**
  - 예를 들어 `스타일의 수정 요청이 여러 번 반복되면` 요청을 `대기열에 모아 두고` **마지막에 한꺼번에 처리한다.**

#### 주요 노드 객체

Node | constructor | nodeName | nodeValue | nodeType
---|:---:|:---:|:---:|:---:|
`문서 노드`   | HTMLDocument | "#document"         | null       | 9
`요소 노드`   | HTMLElement  | 요소 이름(대문자)    | null       | 1
`텍스트 노드` | Text         | "#text"             | 텍스트      | 3
`주석 노드`   | Comment      | "#comment"          | 주석 내용   | 8       
`속성 노드`   | Attr         | 속성이름             | 속성 값    | 2     

#### DOM Tree 계층을 표현하는 프로퍼티

property | 의미
---|---|
`parentNode`        | 이(this) 노드의 부모 노드를 참조한다. Document 객체의 부모 노드는 null
`childNodes`        | 이 노드의 자식 노드의 참조를 저장한 유사 배열 객체(NodeList)
`firstChild`        | 이 노드의 첫 번째 자식 노드, 자식 노드가 없을 때는 null
`lastChild`         | 이 노드의 마지막 자식 노드, 자식 노드가 없을 때는 null
`nextSibling`       | 이 노드와 같은 부모 도드를 가진 이 노드 다음의 형제 노드
`previousSibling`   | 이 노드와 같은 부모 노드를 가진 이 노드 이전의 형제 노드
`nodeType`          | 노드 유형을 뜻하는 숫자(1: 요소 노드, 3: 텍스트 노드, 9: Document)
`nodeValue`         | 텍스트 노드의 텍스트 콘텐트, 요소 노드에서는 null
`nodeName`          | 요소 노드는 대문자로 바뀐 요소 이름이 들억나다. (텍스트 노드: #text)

#### DOM Tree 계층을 가리키는(Tree of HTML Element) 프로퍼티

- DOM트리 안의 `텍스트 노드를 무시하고` HTML 문자에서 요소의 `계층 구조만` 가져오기 위한 프로퍼티가 있다.

property | 의미
---|---|
`childNodes`                | 이 요소와 자식 요소 참조를 저장한 유사 배열 객체(NodeList)
`parentElement`             | 이 요소의 부모 요소 객체를 참조한다.
`firstElementChild`         | 이 요소의 첫 번째 자식 요소 객체를 참조한다.
`lastElementChild`          | 이 요소의 마지막 자식 요소 객체를 참조한다.
`nextElementSibling`        | 이 요소와 같은 부모를 가진 이 요소의 다음의 형제 요소 객체를 참조한다.
`previousElementSibling`    | 이 요소와 같은 부모를 가진 이 요소 이전의 형제 요소 객체를 참조한다.
`childElementCount`       | 자식 요소의 개수 (children.length와 같다.)

## 2. 노드 객체 가져오기

property | return
---|---|
`document.getElementByID(id 값);`                           | 이 요소와 자식 요소 참조를 저장한 유사 배열 객체(NodeList)
`document.getElementsByTagName(요소와 태그 이름);`           | NodeList 객체
`document.getElementsByName(name 속성 값);`                 | NodeList 객체
`document.getElementsByClassName(class 이름);`              | NodeList 객체
`document.querySelectorAll(선택자);`                        | NodeList 객체
`document.querySelector(선택자);`                           | 선택자와 일치하는 요소 개체 중에서 문서 위치가 첫 번째인 요소 객체를 반환

- 여기서 **`NodeList 객체는`** **'살아 있는'** `상태를` 가리킨다. 
  - 즉, 이 객체는 특정 시점의 `정적인 상태를 표현하는 거싱 아니라` **HTML 문서의 변화에 따라 동적으로 바뀐다.**
- **`querySelectorAll은`** HTML 문서의 내용이 바뀌어도 반환한 NodeList값은 바뀌지 않는다.**(정적인 상태를 가져온다.)**
  - `querySelectorAll` 는 일치한 `요소가 없을 때` 빈 NodeList를 반환한다.
  - `querySelectorAll` 과 `querySelector` 메서드는 `:first-line, :first-letter, :link, :visited 의` **`의사 선택자를 지원하지 않는다.`**

### 2-1. Document 객체의 프로퍼티

- Document 객체의 요소를 읽고 쓰기 위한 프로퍼티들 이다.
- embeds,plugin,script는 HTML5의 구성요소로 새롭게 추간되었다.
- **`HTMLCollection객체는`** 유사 배열 객체이며 읽기 전용이다. 
  - HTMLColletion 객체의 요소는 배열 요소의 인덱스 뿐만 아니라 id 속성값, name 속성 값으로 참조할 수 있다. 

property | 의미
---|:---:|
`document.documentElement`                | 문서의 루트 요소(html 요소) 객체의 참조
`document.head`                           | 문서의 head 요소 객체의 참조 
`document.body`                           | 문서의 body 요소 객체의 참조
`document.forms[]`                        | 문서 안의 form요소 객체의 참조를 저장한 유사 배열 객체
`document.images[]`                       | 문서 안의 images요소 객체의 참조를 저장한 유사 배열 객체
`document.achors[]`                       | 문서 안의 achors요소 객체의 참조를 저장한 유사 배열 객체
`document.applets[]`                      | 문서 안의 applets요소 객체의 참조를 저장한 유사 배열 객체
`document.links[]`                        | 문서 안의 links요소 객체의 참조를 저장한 유사 배열 객체
`document.embeds[]`                       | 문서 안의 embeds요소 객체의 참조를 저장한 유사 배열 객체
`document.plugins[]`                      | 문서 안의 plugins요소 객체의 참조를 저장한 유사 배열 객체
`document.scripts[]`                      | 문서 안의 scripts요소 객체의 참조를 저장한 유사 배열 객체

- document.embeds와 document.plugins 같은 객체를 참조한다.

## 3. 요소의 속성 값의 읽기와 쓰기

- `HTML` 요소의 속성을 요소 객체와 속성 프로퍼티로 사용할 때는 **소문자로 작성한다.**
- `JS` 요소 객체의 속성 프로퍼티는 **대소문자를 구분한다.**
  - JS에서는 속성 이름이 여러 단어로 구성되었다면 두 번째 이후 단어의 **첫 글자를 대문자로 표기한 프로퍼티 이름을 사용한다.** 
    - accept-charset -> accpetCharset
    - accesskey -> accessKey // form 요소에서 사용할 수 있다.
    - maxlength -> maxLength // input 요소와 textarea 요소에서 사용할 수 있다.
    - tabindex -> tabIndex // 전체 속성(모든 요소에서 사용할 수 있다.)
- `HTML` 속성의 이름 중 **JS 예약어가 사용되고 있다.** 이런 경우에는 속성 이름 **앞에 html을 덧붙인다.**
  - label 의 for 속성을 htmlFor를 사용한다.
    - class -> className

1. READ (속성 값의 읽기)

```js
    요소 객체.속성 이름
```

2. GET (속성 값 가져오기)

```js
    요소 객체.getAttribute(속성의 이름) // 없으면 빈문자열 또는 null
```

3. SET (속성 값 설정)

```js
    요소 객체.setAttribute(속성 이름, 속성 값) // 해당하는 속성이 없을 때는 그 속성을 새롭게 추가한 후에 설정
```

4. CHECK (속성이 있는지 확인하기)

```js
    요소 객체.hasAttribute(속성 이름) // 논리값으로 반환
```

5. DELETE (속성 삭제하기)

```js
    요소 객체.removeAttribute(속성 이름)
```

6. GET Attribute List (전체 속성의 목록 가져오기)

- 요소 객체에는 `attributes 프로퍼티가 정의되어 있다.`
```js
    var list = document.getElementById("controls").firstElementChild.atttributes;
```
- 이 프로퍼티는 **`NamedNodeMap 객체로`** 그 요소에 설정된 모든 속성의 속성 노드 객체가 담겨 있다.
  - NamedNodeMap 객체는 **유사 배열 객체이며 읽기 전용이다.**
  - NamedNodeMap 객체의 요소인 속성 노드 객체의 name 프로퍼티에는 속성 이름이 담겨 있으며, value 프로퍼티에는 속성 값이 담겨 있다.
  - NamedNodeMap 객체의 요소 배열의 인덱스는 물론 속성 값으로도 가져올 수 있다.

```js
    console.log(list["type"].value);
    console.log(list["value"].value);
    console.log(list.onclick.value);
```

### 3-1. HTML속성

<https://www.advancedwebranking.com/html/>

### 3-2. 이벤트 처리기 프로퍼티

<https://developer.mozilla.org/ko/docs/Web/API/Event>

Event | 설명
---|---|
`abort` | 이미지 로딩이 중단될 경우 실행된다.
`blur` | 엘리먼트가 입력 포커스를 잃어버릴 경우 실행된다.
`change` | 폼 엘리먼트가 포커스를 잃고 값이 변경될 경우 실행된다.
`click` | 마우스 버튼이 눌렸다 떼어질 때 실행된다. mouseup 이벤트가 이어서 발생한다. 기본 동작 방식을 취소하려면 false를 반환한다.
`dblclick` | 마우스가 더블클릭될 때 실행된다.
`error` | 이미지 로딩 오류가 일어날 경우 실행된다.
`focus` | 엘리먼트가 입력 포커스를 얻을 경우 실행된다.
`keydown` | 키가 눌렸을 때 실행된다. 취소하려면 false를 반환한다.
`keypress` | 키가 눌렸을 때 실행된다. keydown 이벤트가 이어서 발생한다. 취소하려면 false를 반환한다.
`keyup` | 키에서 손을 뗐을 때 실행된다. keypress 이벤트가 이어서 발생한다.
`mousedown` | 마우스 버튼이 눌렸을 때 실행된다.
`mousemove` | 마우스가 이동할 경우 실행된다.
`mouseout` | 마우스가 엘리먼트에서 벗어났을 때 실행된다.
`mouseover` | 마우스가 엘리먼트 위로 이동할 때 실행된다.
`mouseup` | 마우스 버튼에서 손을 뗐을 때 실행된다.
`resize` | 윈도우 크기가 변경될 경우 실행된다.
`select` | 텍스트가 선택됐을 때 실행된다.
`reset` | 폼 초기화가 요청됐을 때 실행된다. 초기화를 방지하려면 false를 반환한다.
`submit` | 폼 제출이 요청됐을 때 실행된다. 제출을 방지하려면 false를 반환한다.
`load` | 문서 로딩이 완료됐을 때 실행된다.
`unload` | 문서나 프레임셋이 사라졌을 때 실행된다.

## 4. HTML 요소의 내용을 읽고 쓰기

1. innerHTML 프로퍼티

- innerHTML 프로퍼티는 요소 안의 `HTML 코드를 가리킨다.`

2. textContent와 innerText 프로퍼티

- `textContent `프로퍼티는 요소의 내용을 웹 페이지에 표시했을 때의 **텍스트 정보를 표시한다.**
  - textContent 프로퍼티 값은 `지정한 요소의 자식 노드인` **모든 텍스트 노드를 연결한 값이다.**
    - textContent는 script 요소 안의 텍스트를 반환하지만 innerText는 반환하지 않는다.
    - textContent는 공백 문자를 그대로 반환하지만 innerText는 남는 공백문자를 제거한다.
    - innerText는 table, tbody, tr 요소 등의 테이블 요소를 수정할 수 없다.

## 5. 노드 생성/삽입/삭제 하기

1. CREATE Element (요소 생성)

```js
    var element = document.createElement(요소의 이름);
```

- 그러나 DOM 트리의 계층 구조를 뜻하는 프로퍼티(parentNode, childNode 등)값은 모두 null이다.
  - createElement로 생성한 노드 객체는 `메모리에 생성되어 있을 뿐` **문서의 DOM 트리와는 아무런 관계가 없다.**

- 새로운 텍스트 노드 객체를 생성할때는 `createTextNode메서드를 사용한다.`

```js
    var element = document.createTextNode(텍스트);
```
- createElement와 마찬가지로 createTextNode로 만든 노드 객체도 문서의 **DOM 트리와는 아무런 관계가 없다.**

- 노드 객체를 생성하는 주요 메서드

method | 설명
---|---|
`document.createElement(요소 이름)`                | 요소 노드 객체
`document.createAttribute(속성 이름)`              | 속성 노드 객체 
`document.createTextNode(텍스트)`                  | 텍스트 노드 객체
`document.createComment(텍스트)`                   | 주석 노드 객체
`document.createDocumentFragment()`               | 도큐먼트 프래그먼트
`document.importNode(다른 문서의 노드, deep)`      | 다른 문서에 있는 노드를 복사한다. deep을 true로 설정하면 자식 노드까지 복사하고, false로 설정하면 얕은 복사를 한다.
`node.cloneNode(deep)`                      | 노드를 복사한다. deep을 true로 설정하면 자식 노드까지 복사하고, false로 설정하면 얕은 복사를 한다.

1. INSERT (노드 삽입하기)

```js
    요소 노드.appendChild(삽입할 노드) // 요소의 마지막 자식 노드로 삽입한다.
```

- appendChild 메서드로 노드 객체를 삽입하면 그 객체가 DOM 트리에 추가되고 DOM 트리의 각 노드에 계층 구조를 정의하는 프로퍼티(parentNode, childNode 등)가 바뀐다.

- 지정한 자식 노드의 바로 앞에 삽입하기 

```js
    요소 노드.insertBefore(삽입할 노드, 자식 노드)
```

2. DELETE (노드 삭제하기)

```JS
    노드.removeChild(자식 노드)
```

- 이때 `삭제할 수 있는 노드가` 해당 노드의 **자식 노드이다.**
  - 특정한 노드를 삭제하고자 할 때
    - Anode.paretNode.removeChild(Bnode)

3. REPLACE (노드 치환하기)

```js
    노드.replaceChild(새로운 노드,자식 노드)
```

- 이때 `치환 할 수 있는 노드가` 해당 노드의 **자식 노드이다.**
  - 특정한 노드를 삭제하고자 할 때
  - Anode.paretNode.replaceChild(newNode, Bnode)

## 6. HTML 요소의 위치

### 6-1. 뷰포트 (윈도우 좌표계)
- 웹 브라우저에서 문서의 내용을 표시하는 영역
    - 메뉴, 도구 모음, 탭 등을 포함하지 않는다.

### 6-2. 문서 좌표계
- 문서의 왼쪽 위 꼭짓점을 원점으로 하는 좌푝
- 문서는 웹 브라우저 표시 영역(뷰 포트) 안에 표시
- 문서를 스크롤하면 문서 좌표계의 원점이 뷰 포트를 따라 이동한다.
- 문서 좌표계를 따르는 요소의 좌표는 사용자가 문서를 스크롤 해도 바뀌지 않으므로 뷰 포트 좌표계를 따르는 요소보다 다루기 쉽다.
  
### 6-3. HTML 요소 정보 가져오기
 
```js
    var rect = 요소 객체.getBoundingClientRect();
```

- left
- top
- right
- bottom
- width
- height
  
### 6-4. 뷰 포트의 크기 가져오기

```js
    document.documentElement.clientWidth // 뷰 포트의 너비(스크롤 막대의 너비를 포함하지 않음)
    document.documentElement.clientHeight  // 뷰 포트의 높이(스크롤 막대의 높이를 포함하지 않음)
```

- IE9

```js
    window.innerWidth // 뷰 포트의 너비(스크롤 막대의 너비를 포함)
    window.innerHeight // 뷰 포트의 높이(스크롤 막대의 높이를 포함)
```

### 6-5. 스크롤한 거리 구하기

- IE, FireFox 
  
```js
    document.documentElement.scrollLeft // X 축 방향으로 스크롤한 거리
    document.documentElement.scrollTop // Y 축 방향으로 스크롤한 거리
```
- Chrome, Safari, Opera, Edge, Quirks Mode
  
```js
    document.body.scrollLeft // X 축 방향으로 스크롤한 거리
    document.body.scrollTop // Y 축 방향으로 스크롤한 거리
```

- FireFox, Chrome, Safari, Opera, Edge, IE9 > 
  
```js
    window.pageXOffset // X 축 방향으로 스크롤한 거리
    window.pageYOffset // Y 축 방향으로 스크롤한 거리
```

#### 특정 위치로 스크롤하기

- Window 객체의 scrollTo 메서드 문서 좌표 (X, Y)를 인수로 받으며, 뷰 포트 좌표의 원점(표시 영역의 왼쪽 위 모서리)까지 스크롤 합니다.

```js
    window.scrollTop(X,Y);
```

- `웹 브라우저에서는` **스크롤 복원 기능을 꺼야한다.**
  
```js
    if('scrollRestroation' in history) {
        history.scrollRestoration = 'manual';
    }
```

#### 특정 거리만큼 스크롤 하기

- Window 객체의 scrollBy 메서드는 스크롤할 거리를 인수로 받아 문서를 그 거리만큼 스크롤 한다.

```js
    window.scrollBy(dx, dy);
```

#### 특정 요소가 있는 위치까지 스크롤 하기
  
```js
    요소 객체.scrollIntoView(alignWithTop);
```

- 요소 객체의 `scrollIntoView` 메서드는 그 요소가 웹 브라우저의 **`표시 영역에 들어올 때 까지 스크롤 한다.`**
- 인수 `alignWithTop은` 선택 사항으로 **`생략하면 true로 간주한다.`**
  - `true이면` 요소가 표시 영역의 위쪽 끝에 오도록 스크롤 한다.
  - `false이면` 요소가 표시 영역의 아래쪽 끝에 오도록 스크롤 한다.

### 6-6. 성능 이슈

- `요소의` **위치와 크기를 변경하는 작업은** 레이아웃 처리를 촉발하는 행위가 된다.
  - **최적화의 대상이 되지 않는다.**
- `레이아웃을 처리하려면` **부모 요소까지 거슬러 올라가 계산해야 한다.**
  - 이는 렌더링 성능을 현저하게 떨어뜨리는 원인이 된다.
  - 특히 **`position프로퍼티 값이 relative인`** 요소의 크기 등을 수정하려면 `document 루트부터 다시 계산해야 하므로` 그만큼 시간이 걸린다.
  - 웹 페이지의 렌더링 성능을 개선하고자 한다면 요소의 크기 변경과 위치 변경이 영향을 미치는 범위를 염두에 두어야 한다.

## 7. HTML <form>

### 7-1. DOM 메서드로 가져오는 방법

- 개별로 value로 가져와야 한다. 

```js
    var menu = document.getElementById("menu1");
    var optitions = menu.getElementByTagName("option");
    var inputs = document.querySeletorAll("#form1 input[type='radio']");
```

### 7-2. forms 프로퍼티로 form 요소로 가져오기

- 문서 안의 `form 요소 목록은` **Document 객체의 forms 프로퍼티에서도 가져올 수 있다.**
- forms 프로퍼티 값은 **`HTMLCollection`** 객체이다.
- HTMLCollection 객체의 요소는 배열 요소의 인덱스는 물론 id 속성 값, name 속성 값으로 가져올 수 있다.

```js
    document.forms[0] // 인덱스로 가져오기 (비추)
    document.forms.form1 // id 속성 값으로 가져오기

    document.forms.questions // name 속성 값으로 가져오기
    document.questions // name 속성 값으로 가져오기
```

### 7-3. form 요소 객체의 자식 요소 객체 가져오기

- `form 요소 객체` 자체도 유사 배열 객체이며, 해당 폼의 자식 요소인 폼 컨트롤 요소 객체를 배열의 요소로 갖고 있다.
- 배열의 요소는 HTMLColletion 객체와 마찬가지로 배열요소의 인덱스, id,속성 값, name 속성 값으로 가져올 수 있다.

```js
    document.forms.form1[3]
    document.forms.form1.bloodtype
    document.forms.form1.menu1
```

- form 요소 객체는 `elements 프로퍼티도 가지고 있다.`
- elements 프로퍼티도 **`유사 배열 객체이며`**, 해당 폼의 자식 요소인 폼 컨트롤 요소 객체를 배열의 요소로 갖고 있다.

```js
    document.forms.form1.elements[3]
    document.forms.form1.elements.bloodtype
    document.forms.form1.elements.menu1
```

## 8. CSS 제어하기

```js
    요소 객체.style.프로퍼티 이름 = 값
```

- `style` 프로퍼티 값은 **`CSSStyleDeclaration`** 객체 이다.
  - CSS의 프로퍼티 이름에 `하이픈(-)이 없으면` **그 이름을 그대로 사용**
  - CSS의 프로퍼티 이름에 `하이픈이 있으면` 하이픈을 제거하고, **뒤 단어의 첫 글자를 대문자로 바꾼 문자열을 사용한다.**
  - CSS의 프로퍼티 `이름 앞에 하이픈이 있으면` 하이픈을 삭제하고 **그뒤에 이어지는 단어를 소문자로 표기한다.** 
    - `float 프로퍼티만 예외적으로` **cssFloat가 된다.**
    - font-size -> fontSize 
    - background-color -> backgroundColor
    - -webikt-transform -> webkitTransform
- `스타일 시트의 설정보다` **style 속성에 작성된 값을 우선적으로 적용**
- 요소의 `계산된 스타일은` Window 객체의 `getComputedStyle` 메서드로 가져올 수 있다. 
  - `getComputedStyle` 메서드는 style 객체와 마찬가지로 **`CSSStyleDeclaration 객체를`** 반환한다.
  - `CSSStyleDeclaration` 객체는 **'살아 있는'** 상태를 표현 한다.
  - 그러나 style 객체와 달리 `getComputedStyle` 메서드로 가져온 **계산된 스타일은 읽기 전용이다.**

```css
    p {color:red;}
```

```HTML
    <p id="note">..</p>
```

```js
    var element = document.getElementById("note");
    console.log(element.style.color);  
    console.log(element.style.height);
```

- 모두 빈 문자가 채워진다.
- 이것은 인라인 스타일을 지정하지 않았기 때문이다.

```js
    var computedStyles = document.getComputedStyle(element);
    console.log(computedStyles.color); // -> reb(255,0,0)  
    console.log(computedStyles.height);// -> 24px
```

- 이때 표시되는 계산된 스타일의 프로퍼티 값은 절댓값이다.
- 백분율 등의 상댓값은 절댓값으로 바뀐다.
- 글꼴이나 박스 너비처럼 크기를 가진프로퍼티 값의 마짐가 부분에는 "100px"처럼px를 덧붙인 문자열이 들어간다.

### 8-1. 클래스 제어로 스타일 변경

```js
    element.className = "emphasize";
```

- **`classList`** 프로퍼티(IE 10)
  - classList 속성 값은 **`DOMTokenList`** 객체이다.
    - DOMTokenList 객체는 **유사 배열 객체이며 읽기 전용이다.**
    - 이 객체는 HTMLCollection 객체와 마찬가지로 **`'살아있는'`** 상태를 표현한다.
  - `classList` 객체의 배열 요소는 className 프로퍼티 값이 항상 반영된 상태이다.

- DOMTokenList 객체의 메서드

property | return
---|---|
`add(클래스 이름)`          | 요소의 클래스 목록에 해당 클래스를 추가
`remove(클래스 이름);`      | 요소의 클래스 목록에서 해당 클래스를 삭제
`toggle(클래스 이름);`      | 요소의 클래스 목록에 해당 클래스가 없으면 추가하고 있으면 삭제
`contains(클래스 이름);`    | 요소의 클래스 목록에 해당 클래스가 있는지를 뜻하는 논리값을 반환