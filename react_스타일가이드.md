#### 리액트 스타일 가이드 ###

 1.didmout 라이프싸이클을 일관적으로 아래와 같이 정의한다

useEffect(() => {
    console.log('function component didmount');
}, []);

 2.const를 필수적으로 반영한다. 예외로 2단계 이후에 속성이 바뀌는 것들은 let으로 정의한다

 3.this.props, this.state 처럼 길게쓰지 않고 전부 풀어준다

 const { aa, bb } = this.props;
 const { aa, bb } = this.state;

 4.props는 문서화한다. 함수 또는 클래스 import 구문 바로 하단에 주석으로 정의한다

 5.state도 문서화한다. 별도의 저장소에 저장하고 있는 속성은 저장소에 문서화한다

 6.목록에서 key는 필수적으로 전달한다.(가능하면 index는 사용하지 않고 특유의 id가 존재하지 않으면 uuid로 정의한다)

 7.htmlFor, className과 같이 원래 키워드가 존재해서 변형된 이름들을 일관되게 사용하자

 8.<Fragment></Fragment> 보다는 <></>을 사용한다

 9.this를 fix 시키기 위한 화살표 함수를 가능하면 사용하지 않는다

 10.심볼의 장점과 활용도

 11.자료구조의 활용도 : Map, Set, WeakMap...

 12.for in key 확인

 13.