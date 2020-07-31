# 6번째 주

# css
## 반응형 웹 디자인
웹사이트의 레이아웃을 만들 때 모니터 해상도를 고려해야합니다. 예를 들어 가로가 크거나 작으면 그에 따른 가독성에 문제가 발생할 수 있기 때문에 반응형 디자인을 합니다.    
또 요즘은 모바일과 테블릿 등 다양해졌기 때문에 이에 더 신경써야 합니다. 
이러한 문제를 해결하는 방안 중 하나가 반응형 디자인입니다.  
해상도에 따라 가로 크기나 배치를 변경하여 가독성을 높힐 수 있습니다.

### @media
이러한 반응형 디자인을 할 수 있게 해주는 것이 `@media` 입니다.  
`@media`를 사용하기 위해선 `html`의 `<head>`와 `</head>` 사이에
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
위 코드를 넣어주어야 합니다.        

미디어 쿼리는 화면(screen), 티비(tv), 프린터(print)와 같은 `미디어타입(media type)`과 적어도 하나 이상의 `표현식(expression)`으로 구성됩니다. 표현식은 `width`, `height`, `color`와 긑은 `미디어 특성(media feature)`들을 이용하여 그 특성들의 상태에 따라 다른 스타일 시트를 적용할 수 있습니다. 미디어 쿼리는 css3에 포함되어 있으며, 컨텐츠의 변경 없이 주로 화면 크기에 따라 스타일 시트를 달리하여 적절한 모양을 보여줄 수 있습니다.

#### 미디어 타입
```css
@media screen and (max-width: 768px) {
    body {
        ...
    }
}
```
스크린 타입에 사용되는 값은 여러 종류가 있지만 웹 사이트를 만드는데는 위처럼 screen을 사용하거나 all을 사용하는 것이 일반적입니다.
```css
@media (max-width: 768px) {
    body{
        ...
    }
}
```
위처럼 미디어 타입을 생략하면 all이 기본값이됩니다.

#### 미디어 특성
미디어 특성에서 `max-width` 혹은 `min-width`를 가장 일반적으로 사용합니다. 그외 `height`, `color`, `orientation(화면의 가로 세로방향)` 등이 있습니다.

#### 데스크탑 우선(Desktop First) & 모바일 우선(Mobile First)
반응형 웹을 만들때 스타일을 작성하는 기준으로 큰 가로 폭부터 작은 가로폭 순으로 만드는 것을 `데스크탑 우선`이라고 하고, 작은 가로폭부터 큰 가로폭 순서로 만드는 것을 `모바일 우선`이라고 합니다.

##### 데스크탑 우선
큰 가로폭부터 작은 가로폭 순서로 만들고, `max-width` 를 이용합니다.

```css
/* 일반적 기본 시트 */
@media(max-width: 768px) {
    /* 모바일에 사용될 시트 */
}
@media(max-width: 1024px) {
    /* 데스크탑에서 사용될 시트 */
}
```
혹은
```css
/* 데스크탑과 일반 기본에 사용될 시트 */
@media(max-width: 768px) {
    /* 모바일에 사용될 시트 */
}
```

##### 모바일 우선
작은 가로폭부터 큰 가로폭 순서를 만들고 `mix-width`를 이용합니다.
```css
/* 모바일과 일반적인 시트 */
@media(min-width: 769px) {
    /* 데스크탑에 사용될 시트 */
}
```

### pollyfill
미디어 쿼리는 거의 모든 최신 브라우저에서 잘 작동합니다. IE는 9이상부터 지원합니다. 만약 IE8 이하에서도 동작을 해야한다면 `polyfill`을 사용해야합니다.
`polyfill`은 웹 개발에서 오래된 브라우저가 지원하지 않는 특성을 지원하게 해주는 기술입니다. `respond.js`는 IE8 이하에 미디어 쿼리를 사용하게 해주는 polyfill입니다. 이 라이브러리는 미디어 쿼리를 100% 지원해주진 못합니다.     
`respond.js`는 IE6~8 버전에서 미디어 쿼리를 해석할 수 있도록 만들어주는 자바스크립트 라이브러리 입니다. MIT 라이센스로 배포합니다.      
[respond.js] : https://github.com/scottjehl/Respond/        
미디어 쿼리를 불러오기 위해서 `@import`와 `<style>`요소는 사용할 수 없습니다. `<link>`로 미디어 속성을 사용하거나 `<link>` 요소로 불러오는 스타일 시트 내에 미디어 쿼리를 기술하면 됩니다.      
<br>
스타입 시트와 respond.js 를 포함하는 부분입니다. 이 부분에는 IE 조건부 주석을 사용하였습니다. 이 주석은 IE 에서는 의미가 있고 다른 브라우저에서는 주석으로 처리됩니다. `[if lte IE 8]`은 IE 8 보다 작거나 같은 버전에서 실행된다는 의미입니다.

```html
<link rel="stylesheet" type="text/css" href="./main.css" />
<!--[if lte IE 8]>
<script type="text/javascript" src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js>
<![endif]-->
```

### 크로스 브라우징
어떤 브라우저에서 웹 페이지가 깨지지 않고 정상적으로 나오게 하는 작업       
<br/>
각 브라우저는 페이지를 렌더링 해주는 `레이아웃 엔진` 또는 `렌더링 엔진`을 가지고 있습니다. 주요 엔진의 종류는 아래와 같습니다.
- 트라이던트 (Trident) : MS의 레이아웃 엔진 (IE 시리즈, OutLook 등)

- 게코 (Gecko) : Mozilla 재단의 레이아웃 엔진 (FireFox, ThunderBird)

- 웹킷 (Webkit) : 초기에 Apple이 개발, 차후 웹킷 프로젝트로 분리(Safari, 예전 Chrome, iOS 및 Android 기본 브라우저)

- 프레스토 (Presto) : 오페라 소프트웨어의 엔진 (Opera Browser ~14)

- 블링크 (Blink) : 구글이 개발, 애플의 웹킷에서 파생. 오페라가 사용 (Chrome, Opera 15~)

- 듀얼 엔진 : 두 개의 엔진을 번갈아 사용하는 방식 (고속모드/호환모드)

브라우저는 각 엔진 별로 자체 css 스타일을 가지고 있습니다.      

특히 IE는 버전 별로 렌더링 차이가 심해서 IE를 버전별로 맞춰주어야 합니다.   
방법은 아래와 같은 IE핵 을 사용하거나, 
```html
<!--[if IE 8]>
<link rel="stylesheet" type="text/css" href="./IE8.css" />
[if lt IE 8]
<link rel="stylesheet" type="text/css" href="./IE6-7.css" />
<![endif]-->
```
혹은 `meta`를 이용해서 브라우저 렌더링을 하는 방법이 있습니다.
```html
<meta http-equiv="X-UA-Compatible" content="IE=7" />
```

