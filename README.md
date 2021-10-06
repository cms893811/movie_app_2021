# 최재학 202030432
## [10월 01일]
> 
- 6초 후 문자 출력
```
import React from "react";

class App extends React.Component {
  state = {
    isLoading: true,
  };

  componentDidMount() {
    setTimeout(() => {
      this.setState({ isLoading: false });
    }, 6000);
  }

  render() {
    const { isLoading } = this.state;
    return (
      <div>
        <h1>{ isLoading ? 'Loading...' : 'We are ready' }</h1>
      </div>
    )
  }
}

export default App
```
- componentDidMount()를 쓴 이유: 초기 렌더링이 끝난 후에 작동하게 하기 위해(?)
- npm install axios : axios 설치
- 크롬 JSON viewer 설치
- https://yts.mx/api/v2/list_movies.json 확인
- API 호출
```
import axios from "axios";

componentDidMount() {
    axios.get('https://yts-proxy.now.sh/list_movies.json');
  }

```
- axios는 네트워크를 사용하므로 느리게 동작함
- axios.get()이 반환한 영화 데이터를 받기 전에 끝나므로 실행을 분리하고 async, await을 사용
- async : 비동기라 알려 기다리게 함(?)
- await : axios.get()의 실행 완료를 기다렸다 진행하게 함
- ES6부터 객체의 키와 대입할 변수의 이름이 같다면 코드를 축약할 수 있음.
- 예) { movies: movies } -> { movies }


## [09월 29일]
> prop-types, state
- master branch를 main branch로 변경
인종차별의 뉘앙스를 지우기 위해 변경
- 이후 Git에서 브랜치를 사용자가 설정할 수 있도록 변경되고 Github에서도 기본 브랜치를 master에서 main으로 변경함
- master Branch를 main Branch로 변경
```
git config -global init.defaultBranch main
```
- 기존 Branch 변경
```
git branch -m 현재Branch 바꿀Branch
```
- 리액트 프로젝트 클론 순서
```
git clone 주소
//모듈 다운
npm install
//실행
npm start
```
<br>
정의한 props의 값이 컴포넌트에 전달되지 않는 경우 props를 검사하는 방법이 필요함.

- props를 검사하는 방법
```
// prop-types 설치
npm install prop-types
```

<br>

```
//foodLike에 입력한 값이 데이터베이스에서 넘어온 값이라고 가정

import PropTypes from 'prop-types';
//foodLike 배열의 각 요소에 rating을 추가, 자료형은 Number
rating: 5.0
rating: 4.9
<h4>{rating}/5.0</h4>
rating={dish.rating}
Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired, // string -> number로 수정, string이라 에러표시
}
```

- isRequired 제거 시 필수가 아니여도 되는 항목이 됨

### state
- props는 정적인 데이터만 다룰 수 있다.
- state는 동적인 데이터를 다루기 위해 사용
- state는 class형 컴포넌트에서 사용된다.
#### 클래스형 컴포넌트 작성하기
```
import React from "react";

class App extends React.Component {
  state = {
    count: 0,
  };

  render() {
    return (
      <h1>This number is: {this.state.count}</h1>
    )
  }
}

export default App
```

#### state에 count값 추가하고 사용
- class안에 state={}라고 작성하여 state를 정의
- state는 객체형태의 데이터
- 리액트는 state를 직접 변경하지 못한다. 원래 리액트는 state가 변경되면 render()함수를 다시 실행하여 변경된 state를 화면에 출력하지만 state를 직접 변경하는 경우에는 render() 함수를 다시 실행하지 않음
```
import React from "react";

class App extends React.Component {
  state = {
    count: 0
  };
  
  add = () => {
    this.setState(current => ({
      count: current.count + 1
    }));
  };

  minus = () => {
    this.setState(current => ({
      count: current.count - 1
    }));
  };

  render() {
    return (
      <div>
        <h1>The number is: {this.state.count}</h1>
        <button onClick={this.add}>Add</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    )
  }
}

export default App
```
### 생명 주기 함수
<img src="img.png">

### 클래스형 컴포넌트
#### constructor() 함수
- constructor()는 Component를 생성할 때 state 값을 초기화하거나 메서드를 바인딩할 때 사용한다.
- 생성자 내에서는 setState를 사용하지 않고, this.state를 사용하여 state의 초기값을 할당한다.
- 생성자 내에서는 외부API를 직접 호출할 수 없다. 필요 하다면 componentDidMount()를 사용한다.
```
componentDidMount() {
  console.log('component rendered');
}
```
## [ 09월 15일]
> 
- 리액트는 <APP />와 같은 표시를 컴포넌트로 인식하고, 컴포넌트가 반환하는 값을 화면에 그려준다.
- 리액트는 컴포넌트와 함께 동작하고 리액트 앱은 모두 컴포넌트로 구성됨
- App 컴포넌트는 create-react-app이 자동으로 만들어 주는 기본 컴포넌트
- Potato 컴포넌트 생성
```
import Reacte from 'react';
// 리액트가 JSX를 이해할 수 있게 함
function Potato() {
    return <h3>I love potato</h3>; // html이 아니라 JSX
}
export default Potato;
// 다른 파일에서 Potato 컴포넌트를 사용할 수 있게 함
```
- Potato 컴포넌트 사용
리액트는 최종으로 단 한개의 컴포넌트를 그려야 함
```
App.js 수정
import Potato from './Potato'; //추가
function App() {
  return (
    <div>
        <h1>Hello</h1>
        <Potato /> // 추가
    </div>
  );
}
```
## [ 09월 08일]
> 
- MOVIE_APP_2021 생성
- 파일의 사용하지 않는 부분 삭제
- 리액트 앱 실행, 종료 및 깃 허브 업데이트
- ReactDOM.render(<App />, document.getElementById('root));
아이디가 'root'인 엘리먼트에 App 컴포넌트를 그린다.
- npm start 로 리액트 앱 실행