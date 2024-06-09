# REACT

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
// 리액트 앱 성능 측정 용도 파일
//import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  // 리액트 앱 내부의 잠재적인 문제를 검사하는 도구
  //<React.StrictMode>
    <App />
  //</React.StrictMode>
);
```

## 🔈 컴포넌트 (Componen)

<aside>
💡 재 사용이 가능한 각각의 독립된 모듈(module)을 뜻한다.
- 컴포넌트 함수 이름의 첫글자 : 대문자

</aside>

- 함수 선언식
    
    ```
    function Header() {
      return (
        <header>
          <h1>header</h1>
        </header>
      );
    }
    ```
    
- 화살표 함수
    
    ```
    const Header = () => {
      return (
        <header>
          <h1>header</h1>
        </header>
      );
    };
    ```
    

---

## 🔈 JSX

<aside>
💡 **JavaScript + HTML 태그를 섞어 사용**하는 문법 (자바스크립트 XML)

</aside>

- W3C에서 개발된, 다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어
- ***XEL(eXtensible Markup Language)**

### JSX 닫힘 규칙

- 컴포넌트를 반환하는 HTML 태그는 닫는 태그를 반드시 표기
- ex) `<img />`, `<input />`

```jsx
function App() {
  return (
    <div className="App">
      **<Header />**
    </div>
  );
}
```

### **JSX 스타일링**

인라인 스타일링 (카멜 표기법(fontSize)), 스타일 파일분리

```jsx
// 인라인 스타일링
<div style={{backgroundColor:"#333", fontSize:"16px", color:"#fff"}}>
      <h2>body</h2>
</div>

// 스타일 파일분리
import "./Body.css";
...
 <div className="body">
...
```

---

### 🔈 **산술/문자열/논리 표현식**

```
    const numA = 1;
    const numB = 2;
    const strA = "안녕";
    const strB = "리액트";
    const boolA = "true";
    const boolB = "false";
    return (
        <body>
            <h1>body</h1>
            <h2>총합 : {numA + numB}</h2>
            <h2>{strA + strB}</h2>
            <p>상태 : {**String**(boolA || boolB)}</p>
        </body>       
    );
}
```

### 🔈 **최상위 태그 규칙**

- JSX가 반환하는 모든 태그 : 최상의 태그로 감싸야된다.
- HTML 태그를 최상위 태그로 사용X : `<React.Fragment>` , `<></>`(리액트가 제공기능)
    
    ```jsx
    
    import React from "react";
    // body.js에서 라이브러리를 불러와야한다.
    function Body() {
        return (
            <React.Fragment>
                <div>div 1</div>  
                <div>div 2</div>
            </React.Fragment>    
        );
    }
    ```
    

### 🔈 조건부 렌더링

- 삼항 연산자 (코드 간결, 다중 조건작성 효율↓ , 자주 사용시 가독성↓ )
    
    ```jsx
        const num = 19;
        return (
            <>
                <h2>
                    {num}은(는) {num % 2 === 0 ? "짝수" : "홀수"} 입니다.
                </h2>
            </>
        );
    ```
    
- 조건문 (가독성 ↑, 작성 코드多, 중복 코드 발생 우려)
    
    ```
        const num = 19;
        if (num % 2 === 0) {
            return <div>{num}은(는) 짝수 입니다.</div>
        } else {
            return <div>{num}은(는) 홀수 입니다.</div>
        }
    ```
    

---

## 🔈 **프로퍼티** Props (Properties)

<aside>
💡 상위 컴포넌트가 하위 컴포넌트에 값을 전달할때 사용 (단방향 데이터 흐름)

</aside>

**여러 개의 값 전달**

```jsx
// App.js
function App() {
  const name = "원동인";
  return (
    <div className="App">
      <Header />
      <Body name={name} location={"서울시"} />
      <Footer />
    </div>
  );
}
```

```jsx
// Body.js
function Body(props) {
    console.log(props);
    return <div className="body">{**props.name**}은 {**props.location**}에 거주중</div>
}
```

**구조 분해 할당** (결괏값 객체 → 상숫값(원동인, 서울시))

```jsx
// Body.js
function Body(props) {
		// 구조 분해
    **const { name, location } = props;**
		// 원동인, 서울시
    console.log(name, location);
    return (
        <div className="body">
            {name}은 {location}에 거중합니다.
        </div>
    );
}
```

**스프레드 연산자**

```jsx
// App.js
function App() {
  const BodyProps = {
    name: "원동인",
    location: "서울시"
  };
  return (
    <div className="App">
      <Header />
      **<Body {...BodyProps} />**
      <Footer />
    </div>
  );
}
```

배열객체 추가 (`.length` 요소의 개수)

```
// App.js
function App() {
  const BodyProps = {
    name: "원동인",
    location: "서울시",
    favorList: ["돈", "코딩", "React"]
  };
...
// Body.js
function Body({name, location, favorList}) {
	console.log(name, location, favorList);
	return(
		{name}은 {location}에 거주중 
		<br/>
		{favorList.**length**}개의 흥미
	);
};
```

### **`.defaultProps`**

- **Props의 값 중 특정 값이 전달되지 않았을 때 오류 방지**
    
    ```jsx
    // Body.js
    Body.defaultProps = {
        favorList: [],
    		// console.log : 값이 없을때 -> [] 표기 
    };
    export default Body;
    ```
    

---

### 🔈이벤트 핸들링

```jsx
// html, javascript : 이벤트 핸들링
<button onClick="press()">

// react : 이벤트 핸들링
<button onClick={prss}>클릭</button>
```

이벤트 객체(e)

```jsx
    function clickEvent(e) {
				// 이벤트 객체(e)
				cosnole.log(e);
        console.log(e.target.name);
    }
    return (
        <div className="body">
            <button onClick={clickEvent} name="A버튼">A버튼</button>
            <button onClick={clickEvent} name="B버튼">B버튼</button>
        </div>
    );
```

---

### 🔈State : 상태

**useStage의 용법**

```jsx
const [light, setLight] = useState('off');
// State변수 , set함수(상태업데이트) = 생성자(초깃값)
```

**set함수로 State값 변경** 

```jsx
function Body() {
    const [count, setCount] = useState(0);
    const click = () => {
        setCount(count + 1);
    };
    return (
        <div className="body">
            <h2>{count}</h2>
            <button onClick={click}> + </button>
        </div>
    );
}
```

**State 간소화**

```jsx
// 기존    
    const [name, setName] = useState("");
    const [gender, setGender] = useState("");
    const [date, setDate] = useState("");
    const [text, setText] = useState("");

// 간소화
    const [state, setState] = useState({
        name: "",
        gender: "",
        date: "",
        text: "",
    });
```

---

### **🔈`onChange` 이벤트**

input요소의 `onChange` 이벤트 : 입력필드의 값을 변경할때 발생하는 이벤트

```jsx
function Body() {
    const click = (e) => {
        console.log(e.target.value);
    };
    return (
        <div className="body">
           <input onChange={click} />
        </div>
    );
}
```

드롭다운 옵션선택 (key 값 = e.target.value)

```jsx
    const [text, setText] = useState('');
    const click = (e) => {
        console.log("변경된 값 : ", e.target.value);
        setText(e.target.value);
    };
    return (
        <div className="body">
            <select onChange={click} value={text}>
                <option key={"1번"}>1번</option>
                <option key={"2번"}>2번</option>
                <option key={"3번"}>3번</option>
            </select>
        </div>
    );
}
```

간소화

```jsx
// 간소화    
		const handleOnChange = (e) => {
        console.log("현재 수정 대상 : ", e.target.name);
        console.log("수정값 : ", e.target.value);
        setState({
            ...state,
            [e.target.name]: e.target.value,
        });
    };
		// 기본
    const nameChange = (e) => {
        setName(e.target.value);
    };
    const genderChange = (e) => {
        setGender(e.target.value);
    };
    const dateChange = (e) => {
        setDate(e.target.value);
    };
    const textChange = (e) => {
        setText(e.target.value);
    };
```

---

### **🔈** Props / State **`onClick` 이벤트**

- **부모 컴포넌트** 리젠더 시 **자식도 함께** 리렌더 (상태/값 변화)

```jsx
function Test({number}) {
    return  <div>{number % 2 === 0 ? <h2>"짝수"</h2> : <h2>"홀수"</h2>} </div>;
}

function Body() {
    const [number, setNumber] = useState(0);
    const pluse = () => {
        setNumber(number + 1);
    };
    const miss = () => {
        setNumber(number - 1);
    };
    return(
        <div>
            <h2>{number}</h2>
            <Test number={number}/>
            <button onClick={pluse}>+</button>
            <button onClick={miss}>-</button>
        </div>
    );
}
```

---

### **🔈 Ref** (Ref-erence)

<aside>
💡 DOM을 선택해 직접 접근하기 위해 **`ref`**를 사용
state로만 해결할 수 없고, **DOM을 반드시 직접 건드려야 할 때 사용**

</aside>

`textRef.current.value() = ""` : 버튼 클릭시 입력 폼 value 값 초기화

```jsx
import { useRef, useState } from "react";

function Body() {
    const [text, setText] = useState("");
    const textRef = useRef();

    const handleOnChange = (e) => {
        setText(e.target.value);
    };  
    const handleOnClick = () =>{
        alert(text);
        **textRef.current.value = "";**
        // textRef.current(textRef가 현재 참고하고있는 돔 요소)의 value 값 : ""
    };
    return(
        <div>
            <input ref={textRef} value={text} onChange={handleOnChange}></input>
            <button onClick={handleOnClick}>작성 완료</button>
        </div>
    );
}
```

`textRef.current.focus();` : 5글자 보다 작을때 버튼 클릭시 다시 텍스트 폼 포커스(focus)

```jsx
    const [text, setText] = useState("");
    const textRef = useRef();

    const handleOnChange = (e) => {
        setText(e.target.value);
    };  
    const handleOnClick = () =>{
       if (text.length < 5){
            **textRef.current.focus();**
       }else{
            alert(text);
            setText('5자리 이상');
       }
    };
    return(
        <div>
            <input ref={textRef} value={text} onChange={handleOnChange}></input>
            <button onClick={handleOnClick}>작성 완료</button>
        </div>
    );
```