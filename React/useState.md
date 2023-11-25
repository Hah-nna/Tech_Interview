# React

## 23. 11. 25

- Hooks
  - useState

---

- 태영

컴포넌트가 가질수 있는 상태이며 상태를 생성하고 업데이트 할 수 있습니다.
업데이트 될때마다 상태가 변경되어 화면이 재 렌더링 됩니다.

useState를 사용 하는 이유
DOM렌더링과 관련 있는 일반변수를 사용하게 되면 렌더링 될때 마다 초기화 되지만 state 를 사용하는 경우 값을 반영하여 업데이트 해줍니다.
기존의 컴포넌트가 새로고짐이 되는 것이 아니기 때문에 state의 최신상태로 새로운 컴포넌트로 갱신해 주는것에 더 가깝습니다.

기존에 state를 복사하여 새롭게 state를 갱신해 주기 때문에 객체의 불변성을 지킬 수 있고, 발생할 오류를 미리 방지할 수 있습니다.
또한 state가 변경되면 알아서 리렌더링 해주기 때문에 훨씬 간결하고 효율적인 상태 관리가 가능합니다.

상태 업데이트 방법
setState 함수를 사용하여 상태를 업데이트 할수 있는데, 새로운 상태 값을 인수로 받아 컴포넌트의 상태를 업데이트하고 컴포넌트를 재렌더링 합니다.

- 하나

# React

## useState

### useState란?

```
const [count, setCount] = useState(0)
```

- 공홈의 정의 : 렌더링 사이에 데이터를 유지하기 위한 state 변수 + state 변수를 업데이트하고 리액트가 다시 컴포넌트를 리렌더링하게 하는 setState로 이루어진 상태관리 훅
- 좀 더 축약한 정의 : 데이터를 저장하고 유지할 수 있는 state를 가지고 setState를 통해 state의 상태를 관리하는 상태관리 hook
- setState는 기존의 state를 복사해 새롭게 state를 갱신 -> 객체의 불변성을 지킬 수 있음 -> 오류들을 미리 방지할 수 있음.
- setState를 통해 state에 변화가 생기면 알아서 리렌더링을 해주기 때문에 훨신 쉽게 상태관리를 할 수 있음

### state, state management

useState가 상태를 관리하는 상태관리 훅이라고 했는데, 여기서 상태는 무엇이고 상태 관리는 무엇일까?

<details>
<summary>state</summary>
<div markdown="1">

<p>

> [props](https://legacy.reactjs.org/docs/components-and-props.html) (short for “properties”) and [state](https://legacy.reactjs.org/docs/state-and-lifecycle.html) are both plain JavaScript objects. While both hold information that influences the output of render, they are different in one important way: props get passed to the component (similar to function parameters) whereas state is managed within the component (similar to variables declared within a function).

리액트 공식홈페이지에서는 props와 state 둘 다 렌더링 결과에 영향을 끼치는 일반 자바스크립트 객체라고 정의함.
즉, 둘 다 컴포넌트의 렌더링에 영향을 미치는 데이터임.

props와 state의 차이점은 props는 부모에서 자식컴포넌트로 내려주는 데이터이며, 내려받은 컴포넌트에서 수정이 불가능함
state는 컴포넌트 안에서 관리되는 (함수에서 선언된 변수처럼) 데이터임. useState 같은 훅을 통해 관리되고 사용자의 인터랙션에 따라 변화함 .

즉, state는 사용자와의 인터랙션을 통해 변화하는 데이터임.
예를 들면 좋아요를 누르면 갯수가 변화한다든지, 장바구니에 제품을 담을 때 제품이 추가되고, 삭제할 때는 제품이 삭제되는 등 사용자와의 인터랙션을 통해 상태가 변화하는 것을 볼 수 있음

</p>

</div>
</details>

<details>
<summary>state management</summary>
<div markdown="2">

<p>그렇다면 왜 상태관리가 필요할까?</p>
<p>프로젝트가 커질 수록 상태가 복잡해지기 때문에 효율적으로 상태를 관리하기 위해서 필요함</p>
<p>예를 들어 여러 컴포넌트에서 같은 state를 공유해야하는 일이 생긴다고 가정함.</p>
<p>상위 컴포넌트에서 state를 관리하고 하위 컴포넌트에게 props로 넘겨주는 방식 사용을 사용하게 되는데, 이러한 방식은 복잡성이 증가함. 또한 하위의 하위 컴포넌트에서도 해당 state를 사용해야한다면 props를 계속 내려주어야함(props drilling 발생). 이는 해당 props가 어디서 왔는지 추척하기 어렵게 만듦. 따라서 유지 보수가 어려워짐. </p>
<p>따라서 상태관리 도구를 사용해 상태를 중앙에서 관리하고, 필요한 컴포넌트에게만 제공함으로써 코드의 복잡성을 줄이고 유지보수를 용이하게 할 수 있음 </p>

</div>
</details>

<details>
<summary>state management tools</summary>
<div markdown="3">

<p>

**recoil**

- 전역 상태관리 라이브러리
- 직관적이고 리덕스에 비해 보일러플레이트가 적음
- 러닝커브가 낮다는 장점

recoil은 atom과 selector를 통해 상태를 관리함
먼저 atom을 정의하고 컴포넌트에서 사용 시 useRecoilState, useSetState 등을 사용해 기존의 리액트에서 상태관리를 하는 것과 비슷하게 사용함.
atom 값이 변경되면 해당 atom을 구독하고 있는 모든 컴포넌트가 리렌더링됨.
recoil의 데이터 방향은 리액트처럼 단방향.

**react-query**

- 서버 상태 관리를 할 때 많이 사용
- 직관적이고 서버에서 데이터를 가져오고 캐싱하고 업데이트, 동기화를 하는데 사용
- react-query의 데이터 흐름도 단뱡향

useQuery(fetch)나 useMutation 훅을 사용해 API 호출 정의를 하고 필요에 따라 자동으로 API 호출을 실행함 -> 해당 useQuery나 useMutation을 구독하는 컴포넌트들은 새로운 데이터로 리렌더링됨.
이때 반환된 데이터는 react query가 관리하는 캐시에 저장됨

</p>

</div>
</details>

### useState와 useRef의 차이점

가장 큰 차이점은 useState는 상태값을 관리하기 위해 사용되고, 상태가 업데이트될 때마다 컴포넌트가 리렌더링되며, UI에 반영이 됨.
반면 useRef는 컴포넌트의 생애주기동안 계속 유지되며, 값이 변경되어도 컴포넌트가 리렌더링되지 않음.

<details>
<summary>예시</summary>
<div markdown="4">

```
import { useRef, useState } from 'react;
import "./styles.css";

export default function App() {
  const [stateCount, setStateCount] = useState(0);
  const refCount = useRef(0);

  return (

    <div className="App">
      <button
        onClick={() => {
          setStateCount((prev) => prev + 1);}}> State</button>
      <button
        onClick={() => {
          refCount.current += 1;}} >Ref</button>
      <br />
      <br />
      <div>useState Count: {stateCount}</div>
      <div>useRef Count: {refCount.current}</div>
</div>
);
}
```

<p>
state버튼을 누르면 useState의 stateCount 값이 증가하고, 렌더링되어 변화된 값이 화면에 적용되는 걸 볼 수 있음(해당 상태가 변경될 때마다 컴포넌트가 리렌더링되어 변경된 상태값이 화면에 반영됨)<p>
<p>하지만 ref버튼을 누르면 변경된 값이 화면에 렌더링되고 있지 않음. useRef 내부적으로는 값이 변경되고 있지만 useRef는 current 값이 변경되어도 컴포넌트를 리렌더링하지 않음. 따라서 화면이 리렌더링되지 않으므로 반영이 되고 있지 않을 뿐임.</p>
<p>state 버튼을 다시 눌러 컴포넌트를 리렌더링을 시키면 useRef의 값도 올라감. state가 변경되었을 때, refCount.current의 값도 마찬가지로 화면에 렌더링됨.</p>
<p>useRef는 컴포넌트의 생애주기 동안(언마운트 되기 전까지) 변화하는 값을 가지고 있다가 다른 상태 변경(ex: useState, useReducer 등)으로 인해 컴포넌트가 리렌더링되면 그 시점에서의 최신 refCount.current의 값이 화면에 렌더링됨(useState와 다르게 current의 값이 변화할 때마다 화면 리렌더링x).</p>

</div>
</details>

### useState의 불변성

- setState는 기존의 state를 복사해 새롭게 state를 갱신 -> 객체의 불변성을 지킬 수 있음 -> 오류들을 미리 방지할 수 있음.
- 예를 들면 useState를 통해 불변성을 유지하지 않고 임의로 상태를 변경하면 리액트가 상태 변경을 알아채지 못해 컴포넌트가 불필요하게 재렌더링되거나 혹은 이전 상태와 현태 상태를 리액트가 비교하지 못해 변경된 상태를 UI에 반영하지 못함.
- 따라서 아래와 같은 방식으로 불변성을 지키면서 값을 변경해야 함

<details>
<summary>예시</summary>
<div markdown="5">
<p>
const [item, setItem] = useState(['apple', 'banana', 'orange'])라는 배열을 가진 state가 있다고 가정함
여기에 'peach'를 추가한다고 했을 때 item.push('peach')를 한다면 직접 변경을 하는 것이기 때문에 리액트는 item 배열의 변화를 알지 못함(변경을 할 떄는 setState를 사용해 이전 상태와는 별개의 새로운 상태를 생성하기 때문)
따라서 불변성을 유지하면서 상태를 변경하려면 리액트에서는 다음과 같이 할 수 있음

```
setItem([...item, 'peach'])
```

스프레드 연산자를 사용해 기존 item의 요소들을 새로운 배열에 복사 후 'peach'라는 새로운 요소를 새로운 배열에 추가함. 그러면 기존 item배열은 변하지 않고 기존의 item 배열과는 별개의 새로운 배열이 생성되어 state가 업데이트 됨

</p>
</div>
</details>

---

## 정리

### useState란?

- 데이터를 저장하고 유지할 수 있는 state를 가지고 setState를 통해 state의 상태를 관리하는 상태관리 hook
- setState는 기존의 state를 복사해 새롭게 state를 갱신 -> 객체의 불변성을 지킬 수 있음 -> 오류들을 미리 방지할 수 있음.
- setState를 통해 state에 변화가 생기면 알아서 리렌더링을 해주기 때문에 훨신 쉽게 상태관리를 할 수 있음

### 상태란?

컴포넌트 안에서 관리되고, useState 같은 훅을 통해 관리되며 사용자의 인터랙션에 따라 변화하는 데이터

### 상태관리란?

state를 props로 내려주는 방식을 사용하면 props drilling이 발생해 코드가 복잡해지고, 유지보수가 어려워짐 -> 상태관리 도구를 사용해 상태를 중앙에서 관리하고 필요한 컴포넌트만 사용하게 하여 코드의 복잡도를 줄이고, 유지보수가 용이하게 함

### 상태관리 툴

- Redux, Recoil, Zustand 등

### useState와 useRef의 차이점

- useState : 상태값을 관리하기 위해 사용되고, 상태가 업데이트될 때마다 컴포넌트가 리렌더링되며, UI에 반영이 됨.
- useRef : 컴포넌트의 생애주기동안 계속 유지되며, 값이 변경되어도 컴포넌트가 리렌더링되지 않음.

### useState의 불변성

state가 객체나 배열 등의 참조형 데이터인 경우, 기존 상태를 직접 수정하는 것이 아니라 새로운 상태를 생성해주어 불변성을 유지하게 함 -> 불변성을 유지함으로써 React는 상태의 변화를 효율적으로 감지하고 필요한 컴포넌트만을 재렌더링할 수 있음
