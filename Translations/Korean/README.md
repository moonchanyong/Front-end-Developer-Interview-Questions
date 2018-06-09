# 프론트엔드 면접 문제 은행

이 파일에는 잠재적인 프론트엔드 개발자 후보를 선정할 때 사용할 수 있는 여러 가지 면접 질문들이 있습니다. 후보자에게 모든 문제를 사용하는 것은 많은 시간이 소요되기 때문에 추천하지 않습니다. 대신, 여러분이 요구하는 주요 기술과 관련된 질문들을 몇 가지 선정해서 사용해보세요.
// 흑흑 개발자님이 이거 보고 질문하길..

**참고:** 여기 있는 많은 질문은 자유롭게 추가/수정/삭제될 수 있고 정답보다 그 사람의 능력에 관해 이야기하는 흥미로는 토론을 끌어낼 수 있다는 것을 기억하세요.

## 목차

  1. [일반적인 질문](#일반적인-질문)
  1. [HTML 관련 질문](#HTML-관련-질문)
  1. [CSS 관련 질문](#CSS-관련-질문)
  1. [JS 관련 질문](#JS-관련-질문)
  1. [테스트 관련 질문](#테스트-관련-질문)
  1. [성능 관련 질문](#성능-관련-질문)
  1. [코딩 관련 질문](#코딩-관련-질문)

## 함께하기

  1. [함께하는 분들](#함께하는-분들)
  1. [함께하는 방법](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/master/CONTRIBUTING.md)
  1. [라이선스](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/master/LICENSE.md)

#### 일반적인 질문:

* 어제/이번 주에 무엇을 공부하셨나요?
  + 개인공부 + 면접 공부 + 학교 시험공부하느라 죽음의 주를 보냇습니다. (오늘날자는 6/9)

* 코딩을 할 때 당신을 들뜨게 하거나 흥미를 끄는 것들은 무엇은 가요?
  + 공부하고 있는것을 실제 코드에 적용하였을때, 저번 해커톤에서는 이벤트위임이라는 패턴을 몇일 전에 봤는데 마침 써야해서 사용하였는데 그게 너무 재밌었다.
  + 그리고 해커톤에서 집에 돌아오면서 airbnb es6코딩스타일을 보면서 집에왔는데 실제로 써보기위해 크롬익스텐션 웹툰 크롤러를 만들어봤는데 코드가 깔끔해지는것을 느꼇다.
  + 헤헤 그리고 RORO라고 알고는 있었는데 destructing문법을 사용해서 해보니까 잘 맞는거 같다.
  + 세상에 .. 맞네.. es6부터 강력한 패턴이란걸 깨닫는 사람이 있네용
  + RORO 패턴의 장점에 대해 더써보자 [출처는 이곳](https://taegon.kim/archives/8058)
    - 명명된 인수(Named parameter), JS는 명명된 인수를 지원하지않는다(파이썬은 지원햇다. karg) 그래서 이렇게 명명인수를 사용하다면 더 깔끔하게 넣을 수 있다.
    ```javascript
    // not RORO
    function notRORO(a, b, c) {
      // dosomething
    };

    // 인자가 무엇인지 명확하게 보이지 않는다.
    notRORO(1, 2, 3);

    // RORO pattern
    function doRORO({
      a,
      b,
      c,
    }) {
      //dosomething
    }

    // 인지로 무엇을 넣는지 명확하게 보이고  순서에 얽매이지 않는다.
    doRORO({
      a: 1,
      b: 2,
      c: 3,
    });

    // 만약 명명된 이름이 아닌 다른 이름으로 함수내에서 사용하고싶다면.. (내생각과는 조금 달라서 기록해두어야 할 듟 하다.)
    // 파라미터가 앞에오고 뒤에 값에 할당
    function doRORO({
      a,
      b: bb,
      c: cc,
    }) {
      //dosomething
      console.log(bb, cc); // 2,3
      console.log(b, c); // undefined, undefined
    }

    doRORO({
      a: 1,
      b: 2,
      c: 3,
    });

    ```
    - 더 명료한 인수 기본값
    ```javascript

    function notDefault({
      a,
      b: bb,
      c: cc,
    }) {
      //dosomething
      console.log(bb, cc); // 2,3
      console.log(b, c); // undefined, undefined
    }

    notDefault(); // cannot desctructure.. 문제  왜냐하면 아무 객체도 안들어갔기 때문

    function beDefault({
      a,
      b: bb = 100,
      c: cc = 200,
    } = {} ) {
      //dosomething
      console.log(bb, cc);
    }

    beDefault({a: 3}); //100,200

    ```
    - 더 많은 정보 반환
    ```javascript
    //심지어 리턴이 객체이므로 간단하게 정보를 반환 받고 많은 정보를 받을 수 있다.
    let {a, b, c} = doRORO({a:1, b:2, c:3});
    ```
    - 함수 합성의 용이함 (compose) 이부분은 좌표를 참고하자
    - 추가로 ..

    ```javascript
    // 여기서 파라미터에 b가 들어와있으면 getB가 실행되지않는다.. 이를이용해서 필수 입력값을 지정할 수 있다.
    function requiredParam (param) {
      const requiredParamError = new Error(
        `Required parameter, "${param}" is missing.`
      );

      // preserve original stack trace
      if (typeof Error.captureStackTrace === ‘function’) {
        Error.captureStackTrace(
          requiredParamError,
          requiredParam
        );
      }
      throw requiredParamError;
    }
    function beDefault({
      a = requiredParam('a'),
      b: bb = getB(),
      c: cc = getC(),
    } = {} ) {
      //dosomething
      console.log(bb, cc);
    }

    beDefault({a: 3}); //100,200
    ```


* 최근에 당신이 경험한 기술적인 문제는 무엇이고 그것을 어떻게 해결했나요?
  - 현재 제가 집중하고있는게 펑셔널이랑 면접질문 OS인데 개인적으로 저번 툰로더를 만들때 마주쳣던 이슈 두가지가 있습니다.
  - 첫번째는 cors 두번째는 referer
  - cors는 CORS는 사용자를 대신하여 요청을 허용하고, 악의적인 JS에 의해 만들어진 요청을 차단하고 HTTP 요청을 할 때마다 실행되도록 하는 메커니즘이다. [참조하장](https://github.com/nhnent/fe.javascript/wiki/Jaunary-29---February-2,-2018#access-control-allow-headers)
    + 나온 배경은 원래는 cors가 없었을대는 보안상이유로 다른도메인이 다르면 서로 엔드포인트의 api를 부를 수 없었다.(보안이유 때문에)
    + 하지만 cors는 이를 해결하기위해 사용자를 대신하여 요청을 허용과 차단, http요청을 할때마다 실행 되도록하는 메커니즘
    + 브라우저의 자바스크립트에서 동작하고, 요청을보내고 응답을 받을 수는 있지만 js에서 그 응답에 접근이 안되게한다. (실제로 예전에 해커톤에서 응답만 보내면 되는 경우가있어서 시간이 없어서 cors 문제가 나더라도 동작이되서 놔두었었다.) 이를 해결하기위해 포워딩프록시를 사용하였따~
    + 그렇다면 프록시는 뭐다냐 프락시 서버(영어: proxy server 프락시 서버[*])는 클라이언트가 자신을 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터나 응용 프로그램을 가리킨다.

  - referer Referer 요청 헤더는 현재 요청된 페이지의 링크 이전의 웹 페이지 주소를 포함합니다. Referer 헤더는 사람들이 어디로부터 와서 방문 중인지를 인식할 수 있도록 해주며 해당 데이터는 예를 들어, 분석, 로깅, 혹은 캐싱 최적화에 사용될 수도 있습니다. 네이버 크롤링하는것을 검색해보고 헤더에 referer를 통해서 네이버사이트에서 요청을 하는지 확인하려고 권한확인 하는걸 알아냄

* 웹 애플리케이션이나 사이트를 만들 때 고려해야 할 UI, Security, Performance, SEO, Maintainability에 대해서 설명해주세요.
  + 고통이네 이짊문 ㅡ ㅡ
  + UI 디자이너 같네
    - UI때문에 성능이슈가 발생할 경우가 있다고 생각한다. 예로들어 이미지를 쓸데없이 고해상도로 보내거나, 돔의 개수가 많아서 메모리를 차지하는 부분이 많아지거나.. 이러한 부분을 해결해야한다고 생각한다. 예전에 이미지를 고해상도로 깃헙에 넣어서 만든 동아리 블로그가 있었는데 궁금해서 이를 최적화하기 위한 방법을 찾아보니까 이미지 같은경우는 처음에는 낮은 해상도로 보냇다가 나중에 다른 뷰가 추가되면 고해상도로 바꾸는 등의 작업을 하였다.
    - 그리고 체감성능을 높이기위해서(서버에서 데이터를 요청시 느리다면) 미리 돔을 placehold시켜놓는 방법도 있다.
    - loading 표시를 꼭넣어야한다 ㅡㅡ 꼭 움직이는걸로 ㅡㅡ
    - 뎁스도 깊으면 복잡하게 느껴진다.
  + Security
    - injection(프론트에서도 처리해줘야함)
    - session hijacking
    - cookie는 위험
    - xss (이거 나중에보자 궁금하긴한데 좀 쉬고싶다. )

* 선호하는 개발 환경에 대해 자유롭게 이야기해 주세요.
  - 바닐라 스크립트하고싶습니다. 원래는 jquery를 사용하였다들었는데 다른프레임워크의 의존성을 없애기위해서 바닐라 스크립트로 바꾸셔서 바닐라스크립트로하고싶다.
  - es5보다는 es6가 괜찮습니다.
  - 크로스 브라우징 같은경우에는 can i use를 확인하여 하겠습니다.!!!
  - 앵귤러 사용하긴했지만 더 가벼운 환경이 덜 고통받으니 바닐라 스크립트 괜찮다고 생각합니다!!!
  - 모카 카르마 사용하시는데 TDD하겟습니다!! 테스트 리팩 테스트 리팩!!!

* 버전 관리 시스템은 어떤 것들을 사용해보셨습니까?
  - 깃 만 사용해보았습니다.
  - 대신 깃을 사용할때 풀리퀘스트단위를 적당히 작게 하려고하고 (나중에 유지보수를 위해)
  - 커밋시에는 형식에 맞게 changedAction: description 으로 사용하려고 합니다. 원래는 모듈 네임도 있었지만 어떤 파일이 커밋되는지는 확인 이가능하니까 괜찮다고 생각했습니다.

* 당신이 웹 페이지를 만들 때의 과정을 설명해주실 수 있을까요?
  - 최근 앵귤러로 동아리 사이트를 만들때는 어떻게 만들까 고민해봤는데, 디자인
  - 하나하나 css를 넣는건 힘들거같고 우선 html돔을 넣어놓고 비슷한 다른 페이지에서 사용할 css라면 공통영역에 class로 뽑아서 중복을 최소화 합니다.
  - 로직같은경우에는 DI가 서비스를 통해 가능하고, 페이지에서 공통적으로 사용하게 되는 기능은 서비스로 뺍니다.
  - 그리고 모카 카르마 같은 환경세팅을 했엇는데.. 실제로 빨리 개발해야해서 테스트코드를 많이 작성하지는 못했습니다.
  - 처음으로 환경세팅, CI서버따로 만들고, 개발서버, staging, deploy 서버 따로 만들겠습니다.
  - CI는 깃랩을 사용해보았고, 배포나 개발서버같은경우는 AWS인프라를 사용해보았습니다.
  - 커버리지 90을 목표로 하였습니다.


* 당신에게 5가지 다른 stylesheet가 있습니다. 어떤 방법으로 사이트에 제공하는 게 가장 효과적일까요?
  - 생각나는 방법은 두가지 있습니다..
  - 첫번쨰는 각 파일명으로 클래스네임으로 사용하여. 변경하여 클래스로 변경하여 필요한곳에 섞어서 사용하거나..
* 점진적 향상법(progressive enhancement)과 우아한 성능저하법(graceful degradation)의 차이를 설명하실 수 있습니까?
* 웹사이트에서 assets/resources를 최적화하는 방법에 관해 설명해주세요.
* 브라우저가 한 번에 1개의 도메인에서 내려받는 자원은 몇 개인가요?
  * 예외에는 어떤 것들이 있나요?
* 페이지 로드 시간을 줄이는 세 가지 방법에 관해서 이야기 해 보세요.
* 당신이 프로젝트에 합류했습니다. 근데 그들은 Tab을 이용하고, 당신은 Sapce를 사용했습니다. 어떻게 하실 건가요?
* 간단한 Slideshow 페이지를 만드는 방법에 관해서 이야기해 보세요.
* 만약 당신이 올해 기술적 책임자가 되었다면 무엇을 먼저 하시겠습니까?
* 표준의 중요성에 관해 설명해주세요.
* Flash of Unstyled Content에 관해 설명해주세요. 또 FOUC를 피하기 위해선 어떻게 해야 하나요?
* ARIA와 screenreader에 대해 설명해주세요. 또 접근성을 지원하는 웹사이트를 어떻게 만드는지에 대해도 설명해주세요.
* CSS 애니메이션과 JavaScript 애니메이션의 차이점에 관해 설명해주세요.
* CORS는 무엇의 약자이고 어떤 문제에 대해서 언급하는 것인가요?

#### HTML 관련 질문:

* `doctype`이 무엇을 하는 것인가요?
* 표준모드(standards mode)와 쿽스모드(quirks mode)의 다른 점은 무엇인가요?
* XML과 XHTML의 다른 점은 무엇인가요
* XHTML을 이용한 페이지의 한계점은 무엇이 있나요?
* `application/xhtml+xml`으로 지정한 페이지에 어떠한 문제가 있나요?
* 다국어가 포함된 페이지는 어떤 방식으로 제공하나요?
* 다국어 페이지를 제공하는 여러 방법에 관해 설명해주세요.
* `data-`속성은 무엇을 하는 것인가요? 사용했을 때 이점은 무엇인가요?
* HTML5를 오픈 웹 플랫폼(open web platform)으로 생각해본다면, 어떤 것들로 구성돼 있을까요?
* `쿠키(Cookies)`와 `세션저장소(sessionStorage)`와 `로컬저장소(localStorage)`의 차이점을 설명해주세요.
* `<script>`, `<script async>`와 `<script defer>`의 차이점에 관해 설명해주세요.
* CSS`<link>`를 `<head></head>`사이에 쓰는 것과 JS`<script>`를 `<body></body>`뒤에 사용하는 것은 좋은 사용법일까요? 어디에 배치하는 게 좋을까요?
* Progressive rendering이란 무엇인가요?
* 이미지 태그에 `srcset` 속성을 사용하는 이유는 무엇인가요? 브라우저가 이 속성을 가진 콘텐츠를 평가할 때 사용하는 과정을 설명해보세요.
* HTML templating language를 사용해 본 경험이 있나요?

#### CSS 관련 질문:

* class와 id의 차이점에 관해서 설명해주세요.
* "reset" CSS가 무엇인지, 어떻게 유용한지 설명해주세요.
* Floats가 어떻게 동작하는지 설명해주세요.
* z-index에 관해 설명해주세요.
* BFC(Block Formatting Context)에 관해 설명해주세요
* 클리어링(Clearing) 기술에는 어떤 것들이 있으며, 어떨 때 어떻게 사용하는 것이 적절한지 설명하세요.
* CSS 스프라이트(CSS Sprites)를 설명하고, 페이지나 사이트를 어떻게 향상하는지 설명하세요.
* Image Replacement를 사용해야 할 때, 선호하는 기술과 언제 사용하는지를 설명해주세요.
* 브라우저 스펙 차이에 따른 스타일링 이슈를 수정하기 위해서 어떻게 접근하나요?
* 기능이 제약된 브라우저를 위해서 어떤 방식으로 페이지를 만드나요?
  * 어떠한 기술과 절차를 거치는지 설명하세요.
* 시각적으로 보이지 않고 스크린 리더에서만 가능하게 하는 방법에 관해 설명해주세요.
* 그리드 시스템(Grid system)을 사용한 적이 있나요? 있다면 어떠한 것을 선호하나요?
* 미디어 쿼리(media queries)를 사용한 적이 있나요? 혹은 모바일에 맞는 layout과 CSS를 사용한 적이 있나요?
* SVG를 스타일링하는데 익숙하신가요?
* 인쇄하기 위해 웹페이지를 어떻게 최적화 하나요?
* 효율적인 CSS를 작성하기 위한 "비법(gotchas)"은 어떤 게 있나요?
* CSS 전처리(CSS preprocessors)를 사용해보셨나요?
  * 그렇다면, 사용 경험에 기반을 둬 좋았던 점과 나빴던 점을 설명해주세요.
* 페이지에서 표준 폰트가 아닌 폰트 디자인을 사용할 때 어떤 방식으로 처리하시나요? (웹폰트를 제외하고)
* CSS Selector가 어떠한 원리로 동작하는지 설명해주세요.
* pseudo-elements에 관해서 설명하고 어디에서 사용되는지 이야기해보세요.
* box model에 관해 설명하고 브라우저에서 어떻게 동작하는지 설명해주세요.
* `* { box-sizing: border-box; }`은 무엇이고 사용했을때 이점은 무엇인가요?
* 기억나는 display 속성에 대한 값들을 나열해보세요.
* inline과 inline-block의 차이점은 무엇인가요?
* 요소를 배치하는 방법(relative, fixed, absolute, static) 간의 차이는 무엇인가요?
* CSS에서 'C'는 Cascading을 의미합니다. Cascading에 관해서 설명해주세요. 또 cascading system의 장점은 무엇인가요?
* CSS framework를 사용해본 적이 있으신가요? 실무에서 사용해보았다면 어떤 이점이 있었나요?
* 새로운 CSS Flexbox 혹은 Grid 스펙을 사용해 보신 적 있나요?
* 반응형(Responsive) 디자인은 적응형(Adaptive) 디자인과 어떤 차이점이 있나요?
* 레티나 그래픽 환경에서 작업해 보신 적이 있나요? 하셨다면 어떤 기술을 사용하셨나요?
* *절대 좌표*대신 `translate()` 혹은 반대로 사용하는 이유가 있나요? 있다면 이유에 관해서 설명해주세요.

#### JS 관련 질문:

* event delegation에 관해 설명해주세요.
* `this`는 JavaScript에서 어떻게 작동하는지 설명해주세요.
* prototype 기반 상속은 어떻게 하는지 설명해주세요.
* AMD와 CommonJS는 무엇이고, 이것들에 대해 어떻게 생각하시나요?
* 다음 코드가 즉시 호출 함수 표현식(IIFE)로 동작하지 않는 이유에 관해서 설명해보세요: `function foo(){ }();`.
  * IIFE로 만들기 위해서는 어떻게 해야 하나요?
* `null`과 `unedefined` 그리고 `undeclared`의 차이점은 무엇인가요?
  * 두개를 구분하기 위해서는 어떻게 하면 될까요?
* 클로져(Closure)는 무엇이며, 어떻게/왜 사용하는지 설명해주세요.
  * 클로져를 만들 때 선호하는 패턴은 무엇인가요? argyle (IIFEs에만 적용할 수 있다)
* 익명함수(anonymous functions)는 주로 어떤 상황에서 사용하나요?
* 당신의 코드를 어떻게 구성하는지? (모듈 패턴, 전통적 상속)
* 호스트 객체(Host Objects)와 네이티브 객체(Native Objects)의 차이점은 무엇인가요?
* 다음 코드의 차이점은 무엇인가요?

```javascript
function Person(){} var person = Person() var person = new Person()
```

* `.call`과 `.apply`의 차이점은 무엇인가요?
* `Function.prototype.bind`을 설명하세요.
* `document.write()`는 언제 사용하나요?
* UA 문자열을 이용하여 기능 검출(feature detection)과 기능 추론(feature inference)의 차이점을 설명하세요.
* AJAX에 관해 가능한 한 자세히 설명하세요.
* AJAX를 사용했을 때의 장단점에 대해 설명해주세요.
* JSON이 어떻게 동작 되는지 설명하세요. (그리고 AJAX와 어떻게 다른지 설명하세요.)
* 기존에 JavaScript 템플릿을 사용한 적이 있나요? 만약에 있다면, 어떠한 방식으로 사용했는지 말씀해주세요.
* "호이스팅(Hoisting)"에 대해서 설명하세요.
* 이벤트 버블링(Event Bubbling)에 대해서 설명하세요.
* "속성(Attribute)"와 "요소(property)"의 차이가 무엇인가요?
* 내장된 JavaScript 객체를 확장하는 것이 좋지 않은 이유는 무엇인가요?
* document load event와 DOMContentLoaded event의 차이점은 무엇인가요?
* `==`와 `===`의 차이점은 무엇인가요?
* JavaScript의 "동일출처정책(the same-origin policy)"에 대해서 설명하세요.
* 다음 코드를 동작하게 만드세요.

```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```

* 삼항식(Ternary statement)을 사용하는 이유는 무엇이고, 그것을 표현하기 위한 연산자 단어는 무엇인가요?
* `use strict;`은 무엇이고, 사용했을 때 장단점에 관해서 설명해주세요.
* 100번 반복되는 반복문이 있습니다. 3의 배수일 때는 `fizz`, 5의 배수일 때는 `buzz`, 3과 5의 공배수일 때는 `fizzbuzz`가 출력되는 코드를 작성해보세요.
* 전역 scope를 사용했을 때 장단점에 관해 설명해주세요.
* 때때로 `load` event를 사용하는 이유에 관해 설명해주세요. 또 단점이 있다면 대안에 대해서도 설명해주세요.
* SPA에서 SEO에 유리하도록 만들기 위한 방법에 대해 설명해주세요.
* Promise를 사용해 본 경험이 있나요?
* Promise가 콜백 대비 장/단점은 무엇인지 설명해주세요.
* JavaScript의 작동방식의 장단점에 관해 설명해주세요.
* JavaScript를 디버깅할 때 사용하는 도구가 있으면 설명해주세요.
* 객체 안의 속성과 배열의 아이템을 순회할 때 사용하는 문법에 관해 설명해주세요.
* mutable object와 immutable object에 관해 설명해주세요.
  * JavaScript에서 immutable 객체의 예를 들어보세요.
  * immutability의 장/단점은 무엇인가요?
  * 자신의 코드에서 불변성(immutability를) 어떻게 달성할 수 있나요?
* 동기방식과 비동기 방식 함수의 차이에 관해서 설명해주세요.
* event loop이란 무엇인가요?
  * call stack과 task queue에 관해 설명해주세요.
* `function foo() {}`와 `var foo = function() {}`에서 foo 의 차이가 무엇인지 설명해보세요.
* `let`, `var`, `const`의 차이점에 관해서 설명해주세요.

#### 테스트 관련 질문들:

* test code를 작성하면서 개발하는 방식의 장점과 단점에 대해 설명해주세요.
* test code를 테스트하는 툴을 사용해보신 경험이 있나요?
* 유닛 테스트와 함수테스트의 차이점은 무엇인가요?
* code style linting tool을 사용했을때 장점은 무엇인가요?

#### 성능 관련 질문들:

* 성능관련 이슈들을 발견하기 위해서 사용하는 방법은 무엇인가요?
* 웹사이트 scrolling 성능을 향상시키기 위한 몇가지 방법에 대해 설명해보세요.
* 브라우저의 layout, painting, compositing에 대해 설명해보세요.

#### 네트워크 질문들:

* 전통적으로, 웹사이트의 assets을 여러 도메인으로 서빙했을 때 장점은 무엇인가요?
* URL로 접속했을 때 어떤 플로우로 화면에 웹사이트가 그려지는지 네트워크 관점에서 설명해주세요.
* Long-Polling과 Websocket, Server-Sent Event에 대해 설명해주세요.
* 다음 request header들에 대해 설명해주세요.
  * Diff. between Expires, Date, Age and If-Modified-...
  * Do Not Track
  * Cache-Control
  * Transfer-Encoding
  * ETag
  * X-Frame-Options
* HTTP와 HTTPS에 대해 설명해주세요.
* HTTP Method들에 대해 설명해주세요.

#### 코딩 질문:

*질문: `foo`의 값은 무엇인가요?*
```javascript
var foo = 10 + '20';
```

*질문: 아래 코드의 결과값은 무엇인가요?*
```javascript
console.log(0.1 + 0.2 == 0.3);
```

*질문: 아래 코드가 동작하게 하기 위해선 어떻게 해야할까요?*
```javascript
add(2, 5); // 7
add(2)(5); // 7
```

*질문: 아래 구문의 반환값은 무엇인가요?*
```javascript
"i'm a lasagna hog".split("").reverse().join("");
```

*Question: What is the value of `window.foo`?*
*질문: `window.foo`의 값은 무엇인가요?*
```javascript
( window.foo || ( window.foo = "bar" ) );
```

*질문: 아래 두 alert의 결과값은 무엇인가요?*
```javascript
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
```

*질문: `foo.length`의 값은 무엇인가요?*
```javascript
var foo = [];
foo.push(1);
foo.push(2);
```

*질문: `foo.x`의 값은 무엇인가요?*
```javascript
var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};
```

*질문: 아래 코드의 출력값은 무엇인가요?*
```javascript
console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
console.log('three');
```

#### 그 외 흥미로운 질문들:

* 최근에 수행했던 흥미로운 프로젝트는 무엇인가요?
* 사용하는 개발 도구에서 마음에 드는 부분은 무엇인가요?
* 프론트엔드 커뮤니티에서 당신에게 영감을 준 사람이 있다면 누구인가요?
* 애완동물 관련 프로젝트를 해 보았나요? 해보았다면 어떤 종류의 프로젝트인가요?
* IE에서 가장 좋아하는 기능은 무엇인가요?
* 어떤 커피를 좋아하시나요?

#### 함께하는 분들:

이 문서는 2009년에 다음에 언급된 분들과의 협업으로 시작했습니다.
 [@paul_irish](https://twitter.com/paul_irish) [@bentruyman](https://twitter.com/bentruyman) [@cowboy](https://twitter.com/cowboy) [@ajpiano](https://twitter.com/ajpiano)  [@SlexAxton](https://twitter.com/slexaxton) [@boazsender](https://twitter.com/boazsender) [@miketaylr](https://twitter.com/miketaylr) [@vladikoff](https://twitter.com/vladikoff) [@gf3](https://twitter.com/gf3) [@jon_neal](https://twitter.com/jon_neal) [@sambreed](https://twitter.com/sambreed) [@iansym](https://twitter.com/iansym)

현재는 [100이 넘는 개발자들](https://github.com/h5bp/Front-end-Developer-Interview-Questions/graphs/contributors)이 함께하고 있습니다.
