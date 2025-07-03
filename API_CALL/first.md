## 🧰 0단계. 사전 지식 준비

### 1. HTML/CSS 기본 구조

* **HTML**

  * 문서의 뼈대: `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`
  * 태그 예시: `<h1>`, `<p>`, `<a href="...">` 등
* **CSS**

  * 스타일링: 선택자(selector)와 속성(property):

    ```css
    .btn { background-color: blue; color: white; }
    ```
  * 박스 모델(box model): margin, padding, border

---

### 2. JavaScript 핵심 문법

#### • 변수 선언 – `var`, `let`, `const`

```js
let a = 1;
const PI = 3.14;
```

* `let`: 재할당 가능
* `const`: 재할당 불가 → 상수
* 타입: number, string, boolean, object, array 등
  ([developer.mozilla.org][1])

#### • 함수 (Functions)

```js
function square(x) { return x * x; }
const cube = function(x) { return x ** 3; };
```

* 함수 선언문 vs 함수 표현식
* 파라미터, 반환값, 재귀 호출 가능&#x20;

#### • 객체 (Objects)

```js
const person = { name: "Bob", age: 32, bio() { console.log(`${this.name}, ${this.age}`); } };
person.bio();
```

* 키-값 쌍(property), 메서드(function) ([developer.mozilla.org][2])

#### • 배열 (Arrays)

```js
const arr = [1,2,3];
arr.push(4);
```

* `length`, `push()`, `pop()`
* 반복문(`forEach`, `map`, `filter`) ([developer.mozilla.org][3])

---

### 3. 비동기 처리 (Asynchronous JS)

#### • `fetch`, `Promise`, `async/await`

```js
async function getData() {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    const data = await res.json();
    console.log(data);
  } catch(e) {
    console.error(e);
  }
}
getData();
```

* 네트워크 요청 시 로딩/에러 관리 중요

---

### 4. React 기초 (이후 Next.js의 기반)

#### • 컴포넌트 & JSX

```jsx
function Hello({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

* JSX: HTML-like 문법 + JavaScript 표현식
* 컴포넌트: 재사용 가능한 UI 단위

#### • 상태 관리 – `useState`

```jsx
const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>Increase</button>
```

* 상태 선언 + 변경 함수

#### • 생명주기 & 사이드 이펙트 – `useEffect`

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]);
```

* 렌더 후 실행: 데이터 fetch, 타이머, 이벤트 등 ([w3schools.com][4], [legacy.reactjs.org][5], [codedamn.com][6], [developer.mozilla.org][1])
* 의존성 배열로 재실행 조건 설정
* 깨끗한 코드 유지를 위해 cleanup 함수 활용&#x20;

---

### ✅ Notion 정리 템플릿 예시

#### 📘 Section 1: HTML/CSS

* 목적
* 예시 코드
* Tips

#### 📗 Section 2: JavaScript

* **변수**: 설명 + 예시
* **함수**: 선언 vs 표현식 + 예시
* **객체**: 기본 문법 + 예시
* **배열**: 메서드 리스트 + 예시

#### 📙 Section 3: 비동기 처리

* Promise, async/await 구조
* 예시 fetch 코드 + 에러 처리 설명

#### 📕 Section 4: React

* JSX 설명 + 코드
* `useState`: 상태 개념과 사용법
* `useEffect`: 효과와 cleanup, 예시 코드
