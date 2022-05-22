### react_질의사항 ###

 1.함수형 컴포넌트에서 defaultProps는 어떻게?

 2.number value 0인 경우와 && 으로 컴포넌트 표기했을때의 이슈사항 체크
  -&&, || 연산자로 컴포넌트 렌더링 테스트 ---> null과 undefined 모두 테스트 필요

 3.CustomComponent에 key, ref 정의하기

 4.라이프싸이클 메서드 : 클래스

 5.라이프싸이클 메서드 : 함수형

 6.클래스 컴포넌트에 함수형 함수정의

 7.함수형 컴포넌트에 함수의 위치가 어디가 좋은지 체크

 8.jquery 가이드 필요

 9.this.props.children 예시 체크

 10.resprops 이슈 체크

 11.useEffect시에 2번째 함수에 아무것도 정의하지 않을 경우에 어떻게 되는지 확인

 12.StricMode 필수여부 확인 필요

 13.state는 render에서 사용하지 않아도 render가 되는데 props도 마찬가지인지 확인
  -함수형 컴포넌트도 같이 체크 필요 : 함수형 컴포넌트 자동으로 체크해서 동일하면 수행하지 않음

 14.mousemove에 deferred를 적용

 15.ref 사용방법 1
  -this.InputRef = React.createRef();
  -<input id="id" type="text" ref={this.InputRef} />
  -this.InputRef.current.focus();

 16.HOC 기본 컴포넌트 예시 작성

 17.Context 사용 방법
  -리액트 200제 76, 77

 18.redux
  -리액트 200제 78 ~ 84
  -store를 Provider로 주입받기
  -store를 import로 어디서나 주입받기

19.react-router
 -hash router
 -browser router
 -내부 라우터
 -withRouter 사용시 render 되는 기준은? ---> 중첩 라우팅과 관련이 있는지 재현 필요

20.스크롤 이벤트 debounce 적용하기
 -lodash debounce vs throttle

21.concurrently
 -리액트 예제 112

22.file upload
 -file input
 -axios(ajax)

23.file download

24.효과적인 주석 가이드 필요

25.useState hook 사용법
 -리액트를 다루는 기술 : 챕터 3

26.리액트 이벤트 함수를 화살표 함수인 경우와 아닌 경우를 비교

27.ref 사용방법 2
 <MyComponent ref={(ref) => {this.myComponent= ref}}>

28.useEffect 첫번재 아규먼트에서 함수를 반환시 willUnmount 사이클 처럼 동작하는데 이때 2번째 아규먼트를 주었을 경우와의 차이점과 실제 활용도는 어떻게 되는지 확인 필요

29.useReducer

30.useMemo, useCallback

31.useRef
 용도1.원래 기능의 ref : 실제 dom에 접근하기 위한
 용도2.클래스 컴포넌트에 멤버변수 선언처럼 this.으로 접근하기 위한 다른 방법

32.커스텀 hook

33.sass 사용방법 체크 : node-gyp, ruby 없어도 사용이 가능한지 체크

34.styled-component 가이드 필요
 -컴포넌트 기반 프로젝트 vs 퍼블리싱 위주 프로젝트

35.개발자도구(크롬 플러그인) : react, redux, mobx

36.react-virtualized

37.immer

38.React.memo

39.useContext

40.react-helmet-asnyc

41.함수형 컴포넌트안에 함수 정의시(또는 함수 외부에 함수정의시) 한번만 선언되는지?
 -render가 될때마다 생성되는지?

42.부모 render와 reduce에서 {state...}로 하였을 경우에 최적화가 불가능한지 확인 필요

43.react-redux의 connect 함수 : connect(mapStateToProps, mapDispatchToProps)(연도할 컴포넌트)
 -redux 사용시 명시적으로 호출할지 아니면 props에 상태와 액션 핸들러를 넘겨줄지 확인 필요

44.redux-actions
 -createAction, handleActions

45.useSelector, useDispatch
 -vs connect

46.useStore

47.useActions
 -리액트를 다루는 기술 chapter17

48.redux에서 여러개의 store를 의존하는 컴포넌트만 사용하기 위한 방법은 무엇인지?

49.redux middleware
 -redux-logger
 -redux-thunk

50.ajax 요청과 redux-saga
 -delay, put, takeEvery, takeLatest, select, throttle
 -takeLatest는 응답이 않왔으면 한번만 호출하는 것을 의미하는 것인가?

51.코드 스플리팅
 -await import('')
 -React.lazy
 -Suspense
 -Loadable Components

52.서버 사이드 렌더링
 -ssr-recipe
 -Next.js
 -Razzle

53.useImperativeHandle, useLayoutEffect, useDebugValue

54.useDebounce, useMounted

55.reselect

56.서버 사이드 렌더링 함수
 -renderToString
 -renderToNodeStream
 -renderToStaticMarkup
 -renderToStaticNodeStream

 57.타입스크립트












