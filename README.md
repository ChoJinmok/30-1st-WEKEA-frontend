# :pushpin: 이케해여?

> IKEA 사이트를 모티브 한 가구 커머스 서비스

</br>

## 1. 제작 기간 & 참여 인원

- 2022년 2월 28일 ~ 3월 11일
- 프론트 엔드 : 조진목, 안광민, 유강호
- 백엔드 : 김산, 김광일

</br>

## 2. 사용 기술

#### `Front-end`

- React.js(v17)
- react-router-dom(v6)
- Sass
- JavaScript
- HTML5 / CSS
- Git

#### `Communication`

- GitHub
- Slack
- Trello
- Notion

</br>

## 3. 기능 구현

이 서비스는 가구 커머스 서비스를 목표로 했습니다.  
좋은 고객 경험을 줄 수 있는 기능 위주로 개발하려 했습니다.
저는 팀에서 회원가입, 메인, 로그인, 장바구니, 헤더, 푸터 페이지 등을 개발했습니다.

<details>
<summary><b>기능 구현 설명 펼치기</b></summary>
<div markdown="1">

### 3.1. Sign up 페이지

- **유효성 검사** :pushpin:
  - 많은 input(text, checkbox, radio)정보들이 필요한데 유저가 각 유효성을 파악하기 쉽게 input창을 벗어 날 때와 회원가입 버튼을 눌렀을 때 유효성 검사를 실시해서 화면에 표시했습니다.
    ( [input blur 시 유효성 검사 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/SignupInput.js#L20), [회원가입 버튼 클릭 시 유효성 검사 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L119) )
    - 유효성 검사는 이메일은 이메일 형식으로, 비밀번호는 최소 8자 이상, 대문자, 숫자, 특수문자가 포함돼있는지로 검사했고, 나머지 항목은 필수 항목일 경우 필수로 입력하게끔 유효성 검사를 실시 했습니다.
    - state에서 숫자로 유효성 검사를 표현해줬습니다. (0: 유효성 검사 통과, 1: 필수 항목 미기입, 2: 이메일, 비밀번호 검사)
    - 이메일과 비밀번호는 정규표현식으로 검사해줬습니다.
  - 유저가 어느 부분에서 유효성 검사를 통과못했는지 파악하기 쉽게 useRef를 배열로 관리해서 유저가 유효성 검사 통과에 실패한 input창으로 화면이 focus되는 기능을 구현했고, 유효성 검사에 통과하지 못한 input이 여러개일 때 가장 위의 input으로 focus되게 했습니다.
    ( [focus 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L129) )
    - useRef를 배열로 관리를 해서 focus 기능을 구현했습니다.
    - ref 배열을 순서대로 검사해서 유효성 검사를 통과하지 못한 항목을 발견하면 focus되게끔 했습니다.
- 추 후에 유저의 종류에 따라 다른 서비스를 제공할 수 있게 조건부 렌더링을 통해 두가지 유형의 회원가입을 구현했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/SignupInput.js#L66) )
- 유저가 비밀번호의 텍스트가 제대로 입력했는지 확인할 수 있게 비밀번호를 표시했다가 감출 수 있는 버튼의 기능을 구현했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/SignupInput.js#L41) )
  - JavaScript의 classList toggle을 이용하여 비밀번호 표시 토글 버튼을 구현했습니다.
- 구현하고 관리할 수 있는 부분은 외부에 의존하지 않기위해 외부 페키지나 라이브러리를 사용하지 않고 체크박스를 구현했습니다. ( [전체 체크 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L77), [개별 체크 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L94) )
  - 체크 박스들을 배열로 관리해서 체크 박스 기능을 구현했습니다.

### 3.2. Main 페이지

- **이미지에 포인트** :pushpin: ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js) )
  - 유저가 가구(상품)이 인테리어된 공간을 보면서 가구를 선택할 수 있는 기능을 state를 복합적으로 조합한 조건부 렌더링으로 구현했습니다.
  - 서버에서는 구현이 따로 되지 않아서 [mock data](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/public/data/mainSaleProduct.json)를 구조화 해서 진행했습니다.
  - 마우스가 [포인트 지점에 hover 될 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L18), 마우스가 [포인트 지점에서 벗어날 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L34), 마우스가 [전체 이미지에서 벗어날 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L46), 이렇게 세가지 상황에 맞춰서 기능을 구현했습니다.

### 3.3. Log in 페이지 ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Login/Login.js) )

- 회원가입 페이지와 마찬가지로 유효성 검사를 실시 했습니다.
- 회원가입 페이지와 마찬가지로 비밀번호 표시 유무 번튼을 구현했습니다.

### 3.4. Cart 페이지 ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/cart/Cart.js) )

- 유저에게 웹 어플리케이션으로서 장점을 경험할 수 있게 장바구니에서 유저가 주문 상품의 정보를 변경하면 화면은 프론트단에서 바로 변화 시키고 데이터는 서버로 보내줬습니다.

### 3.5. AsideBar ( [로그인 aside 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/components/Nav/LoginAside/LoginAside.js), [카테고리 aside 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/components/Nav/CtegoryAside/CategoryAside.js) )

- 유저가 단순 웹 사이트가 아닌 웹 어플리케이션을 경험할 수 있도록 메뉴, 회원관리 버튼을 누르면 Aside Bar가 양쪽에서 나오는 기능을 외부 페키지나 라이브러리를 사용하지 않고 CSS만으로 구현했습니다.

### 3.6. Navigation Bar, Footer

- 단순 스타일링 작업

</div>
</details>

</br>

## 4. 핵심 트러블 슈팅

### 4.1. 회원 가입 페이지의 input, check-box(radio-button)들을 하나의 컴포넌트로 모두 관리

#### `트러블 상황`

- 회원 정보에 따라서 차별화된 서비스를 제공하는 기능도 있으면 좋겠다는 마음으로 회원 가입 시 필요한 정보를 많이 담으려고 노력했습니다.
- 그러다 보니 관리해야하는 정보들이 많아 질 수 밖에 없었는데 이를 하나의 컴포넌트로 모든 input들을 다 처리해줄 수 있으면 좋을 수도 있겠다고 생각했습니다.
- check-box와 raido button들도 하나의 컴포넌트로 만들어주려고 했습니다.
- 항목들이 다양해짐([input](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/constantData/inputData.js), [연락수신 checkbox](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/constantData/contactAllowData.js), [필수약관 checkbox](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/constantData/requiredCheckData.js))에 따라 각 항목들이 보여줘아하는 정보도 다양해지고 유효성 검사도 항목별로 각기 다르게 진행했어야했습니다.

#### `트러블 슈팅`

- 각 input들의 name, placeholder을 통한 삼항조건연산자와 단축평가로 렌더링되는 상황과 각 스타일을 다르게 줬습니다.
- check-box와 radio button 컴포넌트의 경우는 type과 className(props), 하위 checkbox항목 유무에 따라 렌더링이 다르게 되도록 구현했습니다.
- 최종 결과 코드: [Signup Input](ttps://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/SignupInput.js), [Check Box & Radio button](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/CheckboxRadio.js#L25)

#### `리팩터링 계획`

- 하나의 컴포넌트(함수)가 모든 상황을 고려하게 하는 것이 얼마나 코드를 지저분하게 만들고 컴포넌트가 무거워질 수 있는지 뼈져리게 느꼈습니다. 거기에 따라 리팩터링을 계획했습니다.
- input가 다양해짐에 따라 종류마다 input에 보여줘야하는 정보도 다양해지고 유효성 검사도 각기 다른 문구를 띄워줘야하는 상황이기 때문에 일단 비슷한 역할을 하는 input들을 나눠서 컴포넌트를 나눠줘야할 것 같습니다.
- 필요하다면 Container 컴포넌트를 만들어서 나눈 각 input 컴포넌트들에 필요한 로직들을 각각 따로 모아서 관리할 것 같습니다.
- 지금은 컴포넌트들이 많이 안나눠져있어서 오히려 가독성이 떨어지는 것 같습니다. 그래서 더 잘게 컴포넌트를 나눠서 '여기서부터 여기까지가 어떤 역할을 하는 부분이다'라는 의미를 더 드러내고 싶습니다.

</br>

### 4.2. 회원 가입 페이지의 유효성 검사

#### `트러블 상황`

- 유저가 유효성 검사 결과를 자연스럽게 알아차릴 수 있도록 각 항목을 벗어날 때, 회원가입 form이 submit될 때 유효성 검사의 결과를 화면에 렌더링 해주고 '회원가입'을 submit할 때는 유효성 검사를 통과하지 못한 항목 중 최상단 항목에 focuc되게끔 기능을 구현하고 싶었습니다.
- 하나의 input 컴포넌트, 하나의 check box & radio button 컴포넌트로 모든 항목들을 관리하고 있어서 유효성과 관련된 state와 ref를 관리해주는 것이 까다로웠습니다.

#### `트러블 슈팅`

- 유효성 검사는 세가지 경우에 대해서 검사를 실시했습니다. ( '필수 항목', 'email', '비밀번호' )
- 유효성 검사 결과는 숫자로 표현해줬습니다. 필수항목을 입력하지 않았을 경우 결과로 숫자 '1' email, 비밀번호 유효성 검사를 통과하지 못한 경우 숫자 '2'로 표현했습니다.
- 유효성 검사는 항목을 구분할 수 있는 값(name, className)에 따라 검사해서 유효성 검사 결과를 state로 관리했습니다. 그리고 결과의 숫자와 항목에 따라 결과를 렌더링했습니다.
- 먼저 각 input 항목을 벗어날 때(blur event) 유효성 검사를 했고, 분기문을 사용하여 각 유효성 검사 결과를 state에 담아주었습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/SignupInput.js#L20) )
- check-box의 경우에는 필수 항목 유효성 검사만 진행하면됐습니다. -> 필수 check-box에 체크를 했다가 다시 풀어줄 경우(blur event) 검사를 실시했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/component/CheckboxRadio.js#L25) )
- 회원가입 제출 버튼을 클릭하면 필수항목인데 입력하지 않았거나 체크하지 않았을 경우의 결과만 검사하면 됐습니다.
  - 반복문과 유효성 검사 결과 state의 key값들을 통해 input value들의 state를 검사해줬고 결과를 유효성 검사 결과 state로 setState해줬습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L119) )
- 회원가입 제출 버튼을 클릭 시 유효성 검사를 통과하지 못한 항목 중 최상단 항목에 focuc되게 하기위해 useRef를 배열로 관리하고 callback ref를 사용했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L224) )
  - ref 배열을 반복문으로 접근해서 각 항목을 검사했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L129) )
  - 필수 항목에만 ref를 전달 해줬는데 전달 안된 항목은 반복문에서 건너띄게했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L130) )
  - 앞에서 8개 항목은 input 그 뒤로는 check-box여서 input은 name으로 바로 접근하고 check-box의 경우 id로 접근했습니다. ( [코드 확인](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Signup/Signup.js#L136) )

#### `리팩터링 계획`

- 유효성 검사의 결과 숫자를 바로 jsx에서 문자로 변환해주다 보니 가독성이 많이 떨어지고 숫자가 무엇을 의미하는지 파악하기가 힘들었던 것 같습니다. -> 숫자로 검사결과를 담는 것이 아니라 바로 문자열로 화면에 보여주고 싶은 메시지를 유효성 결과 state에 담아주고 state를 화면에 보여주는 방식으로 리팩터링 하고 싶습니다.
- 회원가입 제출 함수가 유효성 검사, 포커스, 서버로 데이터 보내기 이렇게 세가지 일을 하는데 각 역할을 함수로 작성해줘서 코드가 어떤 역할을 하는지 명확하게 해주어서 가독성를 높이고 싶습니다.
- 이것 역시 input 컴포넌트를 적절히 나누면 유효성 검사 함수가 훨씬 간결해질 거 같습니다.

</br>

### 4.3. 인테리어 공간 이미지에 좌표 찍기

#### `트러블 상황`

- 사용자가 가구를 고를 때 단순히 가구 이미지만 보고 가구를 선택하는 것이 아니라 인테리어가 이루어진 공간에서 가구를 보고 가구를 선택할 수 있게 하고 싶었습니다.
- 서버에서 api가 구현되지 않아서 mock 데이터를 직접 작성했어야했습니다.

#### `트러블 슈팅`

- 좌표의 개수, 위치, 상품의 정보 등이 필요했고 프론트에서 단독으로 구현하는 것이 아닌 서버에서 이런 정보들이 모두 있어야한다고 판단했습니다. -> [데이터 구조 결정](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/public/data/mainSaleProduct.json)
- 각 인테리어에서 좌표들이 담긴 배열을 만든 후 배열을 jsx에서 화면에 렌더링하는 방식으로 구현했습니다.

### 4.4. 인테리어 공간 이미지 좌표들의 정보는 언제 보여줄것인가?

#### `트러블 상황`

- 인테리어 공간 이미지에서 모든 지점 정보를 보여주면 사용자 입장에서 가독성도 떨어지고 어느 가구의 정보인지 파악하는 것도 힘들겠다 생각했습니다.
- 그래서 각 좌표 지점들 중 처음에 기본값으로 한 지점의 정보를 보여주고 나머지 지점들은 마우스가 좌표에 올라 갔을 때 각 정보를 화면에 보여주는 방식으로 처리해주고 싶었습니다.
- 마우스가 아웃되면 다시 좌표에 해당하는 가구 정보를 보여주지 않고 싶었고 마우스가 인테리어 공간 이미지에서 벗어나면 기본값으로 돌아가서 처음에 보여준 지점의 정보를 다시 보여주고 싶었습니다.

#### `트러블 슈팅`

- 앞서 말한 기능을 구현하려면 어떤 좌표가 처음에 기본값으로 보여주고자 하는 가구인지 서버에 저장돼있어야 판단해서 mock data에 default hover라는 정보를 각 좌표에 추가했습니다.
- [마우스가 각 좌표에 올라갔을 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L18), [마우스가 좌표에서 벗어날 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L34), [마우스가 인테리어 공간 이미지를 벗어날 때](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L46), 이렇게 세가지 경우에 대응할 수 있게 함수를 각각 만들었습니다.
  - 각 함수는 분기문과 반복문을 이용해서 화면에 보일지 말지를 결정했습니다. (defaultHover값이 true일 때 화면에 보입니다.)
- defaultHover가 true일 때 'connectingDotHover' className을 줘서 visibility, opacity을 조정했습니다. ( [CSS 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/component/LinkPoint.scss#L52), [JSX 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/component/LinkPoint.js#L30) )

#### `리팩터링 계획`

- 각 좌표가 이미지에 찍혀있고 각 정보가 화면에 보이는 위치도 서버에서 줘야한다고 판단해서 mock data를 만들었는데 정보 위치는 프론트에서 정해주는 것이기 때문에 굳이 데이터에 들어가 있을 필요가 없을 거 같습니다.
- 마우스 이벤트 함수들이 map 메서드내부에 if문 내부에 for문 내부에 if-else문으로 이어지기 때문에 가독성이 많이 떨어지기 때문에 함수를 좀 더 간결하고 가독성을 높이는 작업을 할 것 같습니다.

  <details>
  <summary><b>리팩터링 예시</b></summary>
  <div markdown="1">

  [원본 코드](https://github.com/ChoJinmok/30-1st-WEKEA-frontend/blob/master/src/pages/Main/Main.js#L18)

  ```javascript
  const hoverDot = (imgIndex, dotIndex) => {
    points[imgIndex].dots.forEach((dot, index) => {
      dot.hover = index === dotIndex;
    });

    setPoints([...points]);
  };
  ```

  </div>
  </details>

</br>

## 5. 그 외 트러블 슈팅

### 5.1. 회원 가입 페이지의 input들을 하나의 컴포넌트로 모두 관리하는 문제

## 6. 회고 / 느낀점

> [프로젝트 개발 회고 글](https://jjmok.tistory.com/entry/%EC%9C%84%EC%BD%94%EB%93%9C-1%EC%B0%A8-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%ED%9A%8C%EA%B3%A0%EB%A1%9D)
