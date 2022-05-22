handleClick = () => {
    console.log('this is:', this);
  }
  ---> this.bind 대체

  onClick={() => this.handleClick()}
  ---> this.bind 대체 : 하지만 콜백함수들이 지속적으로 생성됨

아래의 2가지 경우는 동일하고 : 두 경우 모두 React 이벤트를 나타내는 e 인자가 ID 뒤에 두 번째 인자로 전달됩
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>

import { nanoid } from 'nanoid'; ---> uuid 라이브러리

리스트의 key 속성은 단일에 지정하는 것은 아니고 for(반복)에서 사용하는 것이다

부모에서  React.createRef(); 생성후 자식에 넘겨줄 수 있다

HOC와 forwardRef를 조합해서 부모가 자식에게 ref를 전달할 수 있는가?

자기 자신이 아닌 영역을 클릭했을때의 처리는 아래와 같이 사용할 수 있다
onClickOutsideHandler(event) {
    if (this.state.isOpen && !this.toggleContainer.current.contains(event.target)) {
      this.setState({ isOpen: false });
    }
  }

<Suspense 컴포넌트는 자식 컴포넌트가 모두 로딩전에 fallback으로 지정된 컴포넌트가 보이게끔해주는 컴포넌트이다 
function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </div>
  );
}

보통 Lazy import는 네트워크 리소스를 사용하므로 Suspense 상단에 에러바운더리로 감싸는 것이 좋다

Provider로부터 하위 consumer(.contextType와 useContext을 포함한)로의 전파는 shouldComponentUpdate 메서드가 적용되지 않으므로, 상위 컴포넌트가 업데이트를 건너 뛰더라도 consumer가 업데이트됩니다. ---> 테스트 필요

Context는 Object.is를 통해서 비교한다

기본적으로 하위 컴포넌트에서 Context를 사용은 this.context를 이용하여 사용하는데(이때 적절하게 하나의 context를 찾아서 사용한다) 멀티로 사용하기 위해서는 여러 context를 구독해아하고 특정 Context를 this.context로 사용할려면 아래와 같이 특수하게 정의해줘야 한다. 
 -MyClass.contextType = MyContext; 또는 static contextType = MyContext;으로 정의한다(아직 실험적인 방법임)
부가설명
React.createContext()로 생성한 Context 객체를 원하는 클래스의 contextType 프로퍼티로 지정할 수 있습니다. 이 프로퍼티를 활용해 클래스 안에서 this.context를 이용해 해당 Context의 가장 가까운 Provider를 찾아 그 값을 읽을 수 있게됩니다. 이 값은 render를 포함한 모든 컴포넌트 생명주기 매서드에서 사용할 수 있습니다.


에러가 발생한 뒤에 폴백 UI를 렌더링하려면 static getDerivedStateFromError()를 사용하세요. 에러 정보를 기록하려면 componentDidCatch()를 사용하세요.


ref 전달하기 : 자식에 실제돔을 부모에서 사용하기 위한 방법
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));
// 이제 DOM 버튼으로 ref를 작접 받을 수 있습니다.
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;

#.mixin 방식을 대체하는 예시
var PureRenderMixin = require('react-addons-pure-render-mixin');

var Button = React.createClass({
  mixins: [PureRenderMixin],

  // ...

});
위의 방법을 아래의 방법으로 대체한다
var shallowCompare = require('react-addons-shallow-compare');

var Button = React.createClass({
  shouldComponentUpdate: function(nextProps, nextState) {
    return shallowCompare(this, nextProps, nextState);
  },

  // ...

});

#.minin은 안티패턴이고 HOC로 대체한다

#.HOC 상위 컴포넌트에서 하위 컴포넌트에게 props 전달시에 불필요한 props를 거르고 상위 컴포넌트에서 사용하는 전용 속성은 제거하고 보내는 것이 좋다

#.HOC 하위 컴포넌트의 displayName은 아래와 같은 방법으로 사용한다
function withSubscription(WrappedComponent) {
  class WithSubscription extends React.Component {/* ... */}
  WithSubscription.displayName = `WithSubscription(${getDisplayName(WrappedComponent)})`;
  return WithSubscription;
}

function getDisplayName(WrappedComponent) {
  return WrappedComponent.displayName || WrappedComponent.name || 'Component';
}

#.반대로 false, true, null 또는 undefined와 같은 값들을 출력하고 싶다면 먼저 문자열로 전환 해야합니다.
 -String()

#.Profiler Api가조 존재한다(컴포넌트 방식으로 감쌈)
 -https://ko.reactjs.org/docs/profiler.html

#.ref는 커스텀 클래스에도 매핑이 가능하고 실제로는 커스텀 인스턴스에 정의된 함수를 사용할 수 있음을 의미한다

#.함수형 컴포넌트에서는 ref를 주입받을 수는 없지만 생성해서 사용할 수는 있다
 -const textInput = useRef(null);

#.가능하면 ref를 콜백 함수로 만들어야 한다면 별도의 함수로 지정해서 만든다

#.display 공통화면 필요하다면 HOC 보다는 render props 패턴을 사용하자

#.typescript base로 create-react-app app 생성
 -npx create-react-app my-app --template typescript

#.함수형 컴포넌트 정의 방법 2가지
const Example = (props) => {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}

function Example(props) {
  // 여기서 Hook을 사용할 수 있습니다!
  return <div />;
}

#.최초 render시 호출되는 함수 순서
 -constructor()
 -static getDerivedStateFromProps()
 -render()
 -componentDidMount()

#.최초 이후 update시 호출되는 함수 순서
 -static getDerivedStateFromProps()
 -shouldComponentUpdate()
 -render()
 -getSnapshotBeforeUpdate()
 -componentDidUpdate()

 #.해제될때 호출되는 함수
  -componentWillUnmount()

 #.에러시 호출되는 함수
  -static getDerivedStateFromError()
  -componentDidCatch()

 #.React 라이프사이클 함수
  1.constructor()
  2.componentDidMount()
  3.componentDidUpdate()
  4.componentWillUnmount()
  5.shouldComponentUpdate()
  6.static getDerivedStateFromProps()
  7.getSnapshotBeforeUpate() : 업데이트 render() 이후에 호출되는 함수로 componentDidUpdate 전에 호출된다(좀 더 자세히는 실제 dom, ref를 최신화 하기 직전에 호출된다)
   -render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출된다. componentDidUpdate에 세번째 파라미터인 snapshot 값으로 전달받을 수 있다
  8.static getDerivedStateFromError()
  9.componentDidCatch()

 #.forceUpdate는 shouldComponentUpdate 라이프사이클 단계를 무시한다

 #.[]를 ʻuseCallback`에 종속성 배열로 전달합니다. 이렇게 하면 ref 콜백이 다시 렌더링 간에 변경되지 않음으로 React가 불필요하게 호출하지 않습니다

 #.Hook에서 shouldComponentUpdate를 대신하는 방법은 아래와 같다
 const Button = React.memo((props) => {
  // 여러분의 컴포넌트
});

또는 const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

 #.getDerivedStateFromProps 함수의 반환값은 state에서 사용할 값이며 보통 props를 이용하여 state를 변경하고자 할때 사용되며 필요가 업을 경우 null을 반환하면 된다

 #.Custom Hook을 정의한다는 것은 공유 가능한 함수를 정의하는다는 의미이다 : 모든 기능의 hook을 정의할 필요가 없다

