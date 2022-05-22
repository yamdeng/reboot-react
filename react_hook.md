### Hook ###

 0.useState, useEffect, useContext, useReducer, useRef, useCallback, useLayoutEffect, useMemo, useImperativeHandle

 1.속성, 함수 쌍으로 생성
  -const [count, setCount] = useState(0);
  : count 변수는 state 개념이고 setCount는 state 변경 핸들러

 2.class 선언 방식에서는 hook을 사용할 수 없음

 3.state와 hook의 차이점은 다른 상태 속성을 건드리지 않는 차이점이 있다

 4.useEffect()는 didMount, didUpdate 라이프사이클 역할을 한다
 useEffect(() => {
    // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
    document.title = `You clicked ${count} times`;
  });

 5.willUnmount시 이벤트 핸들러 제거 같은 코드는 이하와 같이 작성한다
 useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

 6.useState(), useEffect() 함수는 각각 한쌍으로 정의가 된다

 7.Custom Hook
  -기본적인 아이디어는 render에서 사용될 속성값을 반환하는 함수를 정의한다

 8.Hook 문법은 2가지 경우에서 사용 가능하다
  8-1.최상위 컴포넌트 레벨
  8-2.Custom Hook 함수

 9.상태값이 변경된 경우에만 useEffect가 반영되게끔
 useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // count가 바뀔 때만 effect를 재실행합니다.

10.커스텀 Hook 함수의 이름은 use로 시작한다

11.Hook에서 Hook으로 정보 전달하기
 -큰 의미는 아니고 useState에서 정의한 속성을 커스텀 Hook 함수의 아규먼트로 전달하면 된다
  : 연계되는데 의미는 변경시마다 함수의 인자로 전달되므로 event가 dispatch 된다고 보면 된다

12.redux(useDispatch, useSelector), react-router 지원 버전
 -redux(v7.1.0), react-router(5.1)

13.state를 전체 object로 사용하는 방법 : setState시에 ...으로 별도로 병합시켜줘야 한다
function Box() {
  const [state, setState] = useState({ left: 0, top: 0, width: 100, height: 100 });
  // ...
}

useEffect(() => {
    function handleWindowMouseMove(e) {
      // "... state"를 spread 하여 너비와 높이가 "손실"되지 않습니다
      setState(state => ({ ...state, left: e.pageX, top: e.pageY }));
    }
    // 주의: 이 구현은 약간 단순화되었습니다
    window.addEventListener('mousemove', handleWindowMouseMove);
    return () => window.removeEventListener('mousemove', handleWindowMouseMove);
  }, []);

 14.이전 상태값 얻어오는 방법
 function Counter() {
  const [count, setCount] = useState(0);

  const prevCountRef = useRef();
  useEffect(() => {
    prevCountRef.current = count;
  });
  const prevCount = prevCountRef.current;

  return <h1>Now: {count}, before: {prevCount}</h1>;
}

15.Hook API
 15-1.useState
 ㄱ.class의 setState 처럼 자동 merge가 아니므로 아래와 같이 별도로 merge를 해줘야 한다
const [state, setState] = useState({});
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
 
 15-2.useEffect
  -특정 속성 변경시 실행 : 배열이 빈 배열이라면 한번만 실행함
  useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);

 15-3.useContext ---> Consumer로 사용됨

 컴포넌트에서 가장 가까운 <MyContext.Provider>가 갱신되면 이 Hook은 그 MyContext provider에게 전달된 가장 최신의 context value를 사용하여 렌더러를 트리거 합니다. 상위 컴포넌트에서 React.memo 또는 shouldComponentUpdate를 사용하더라도 useContext를 사용하고 있는 컴포넌트 자체에서부터 다시 렌더링됩니다.

 15-4.useReducer : action과 state의 조합

 15-5.useCallback : 메모제이션된 콜백을 반환

 15-6.useMemo : 메모제이션된 값을 반환

 15-7.useRef : createRef와 동일

 15-8.useImperativeHandle : forwardRef ---> 부모에서 자식의 dom에 접근하기위한 방법
 
 15-9.useLayoutEffect

 15-10.useDebugValue

 16.useRef가 용도가 실제 dom을 접근하는데만 사용하는 것이 아니고 this에 특정값을 대입해서 유지하고 관리하는데도 사용된다

 17.


