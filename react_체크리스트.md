체크리스트

1.HOC와 forwardRef를 조합해서 부모가 자식에게 ref를 전달할 수 있는가?

2.탭키 입력시 이동은 default로 되는가?

3.React.lazy와 Suspense는 아직 서버 사이드 렌더링을 할 수 없습니다. ===> 서버사이드 렌더링에서는 Lazy 로딩을 지원하지 않는다는 의미인가?
 -서버에서 렌더링 된 앱에서 코드 분할을 하기 원한다면 Loadable Components를 추천합니다

4.Lazy 로딩시 한번 로딩한 자원은 다시 가져오지는 않는지 확인

5.Lazy 로딩을 아래와 같이 라우팅을 정의하는 부분에 정의하면 어떤 절차로 다운로드 해오는지 체크
const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Switch>
        <Route exact path="/" component={Home}/>
        <Route path="/about" component={About}/>
      </Switch>
    </Suspense>
  </Router>
);

6.Lazy 설정시 빌드된 파일은 어떤방식으로(어떤 단위로 파일이 분류되는지) 결과물이 추출되는지 확인

7.함수를 자식으로 받는 패턴에 대해서는 render props을 참조하세요.
 -https://ko.reactjs.org/docs/render-props.html

8.MyContext.Consumer ---> 해당의미를 체크해야 함. 이하는 부가설명
Context.Consumer의 자식은 함수여야합니다. 이 함수는 context의 현재값을 받고 React 노드를 반환합니다. 이 함수가 받는 value 매개변수 값은 해당 context의 Provider 중 상위 트리에서 가장 가까운 Provider의 value prop과 동일합니다. 상위에 Provider가 없다면 value 매개변수 값은 createContext()에 보냈던 defaultValue와 동일할 것입니다.


9.Context 값의 변경의미가 존재하는가? 존재하지 않다면 사용하는 이유가 있는가?

10.React.forwardRef를 사용하는 이유는 무엇이고 HOC와 궂이 사용할 필요가 있는가?
 -https://ko.reactjs.org/docs/forwarding-refs.html

11.라이프사이클 함수 체크 : getInitialState

12.HOC 예시 직접 작성 및 확인 필요

13.아래의 es6 문법 체크
 -const { extraProp, ...passThroughProps } = this.props;
 
14.lodash.flow, lodash.flowRight 함수 예시 체크

15.아래와 같이 사용시 React.createRef를 않해도 되는건가?
 -<select className="Chosen-select" ref={el => this.el = el}>

16.배열자체를 render에서 반환하는게 가능한지 확인
render() {
  // 리스트 아이템들을 추가적인 엘리먼트로 둘러쌀 필요 없습니다!
  return [
    // key 지정을 잊지 마세요 :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}

17.상위 컴포넌트가 변경되었는데 하위 컴포넌트는 변경이 않되었을때 render의 기준이 어떻게 되는지 확인

18.ref는 커스텀 클래스에도 매핑이 가능하고 실제로는 커스텀 인스턴스에 정의된 함수를 사용할 수 있음을 의미한다 ===> 테스트 필요

19.React.createRef(); 생성된 ref 값을 props로 연결해주면 이용이 가능한건가?

20.콜백 함수 방식으로 ref를 생성시에 current로 접근을 않하고 바로 해도 되는가?

21.lifecycle getDerivedStateFromProps 함수는 어떨때 사용하는 것인가?
 -getDerivedStateFromProps

22.구조 할당 방법 재체크
 -https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EB%B0%B0%EC%97%B4_%EA%B5%AC%EC%A1%B0_%EB%B6%84%ED%95%B4

23.useEffect가 didmount, didupdate의 역할을 한다면 didmount에서만 해야하는 일은 어떻게 구분할 것인가?
 -https://codesandbox.io/s/jvvkoo8pq3 예제 확인
 -아마도 mount와 비교하는 방법은 [] 빈배열을 던지면은 최초에만 체크하고 않하는듯 함

24.useReducer는 redux의 reducer를 사용함에 있는가?

25.제네레이터, async, await 체크

26.useLegacyState 사용 case 체크

27.hook detail
 -https://www.robinwieruch.de/react-hooks-fetch-data/

28.Context, Hook bestpractice 체크

29.useCallback도 쌍으로 정의 가능하는 개념인가?

30.useEffect 안에서 사용하는 함수는 useEffect 내부에서 정의하는 함수여야 bestpractice 인가?

31.useState에서 사용하는 상태의 종료가 Object이고 Object의 속성이 변경이 되었을때만 render를 해야한다면 어떻게 해야하는가?

32.useEffect는 전역의 개념인가? 아니면 useState쌍의 개념인가?

33.useCallback : 메모제이션된 콜백을 반환 ---> 실제 용도가 어떻게 되는가?

33.useMemo : 메모제이션된 값을 반환 ---> 실제 용도가 어떻게 되는가?

34.useImperativeHandle : forwardRef ---> 부모에서 자식의 dom에 접근하기위한 방법

35.useEffect와 useLayoutEffect 차이점은 무엇인가?

36.lodash.throttle, lodash.debounce, raf-schd(requestAnimationFrame)

37.아래의 메서드는 각 컴포넌트별로 기본적으로 존재하는 라이프사이클 함수인가?
  -static getDerivedStateFromError()
  -componentDidCatch()

38.render의 여러 case에 대한 시나리오를 검증할 필요가 있음
 1.상위에서 render가 않되었지만 하위가 render가 되는 경우
 2.상위에서 render가 되었지만 하위에서 render가 않되는 경우(또는 안되게 하는 방법)

39.getDerivedStateFromProps 함수의 반환값은 state에서 사용할 값이며 보통 props를 이용하여 state를 변경하고자 할때 사용되며 필요가 업을 경우 null을 반환하면 된다 ---> null 반환시 state 자체를 null로 바꾸게하는건 아닌지 확인 필요

40.array.reduce, reduce

41.array 할당자가 아래와 같이 되는가?
 [...state, {
              id: state.length ? Math.max(...state.map(todo => todo.id)) + 1 : 0,
              name: action.name,
              complete: false
            }]
            : state;

41.react-devtools@^3, react-devtools@^4의 차이점 및 브라우저 확안 플러그인을 다르게 가져가야 하는지 체크





reducer
 -https://velog.io/@zayong/Reducer%EB%9E%80
 -https://devlog.jwgo.kr/2018/08/23/redux-which-is-weird-term/
