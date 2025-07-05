## ✅ 2단계 목표

* 외부 API에서 데이터를 가져와서 화면에 표시
* `fetch` 또는 `axios`로 데이터 호출
* `useEffect`를 사용해 컴포넌트 마운트 시 데이터 가져오기
* 로딩 중 / 에러 처리까지 해보기
* 실제 API(`jsonplaceholder`, `포켓몬 API`)를 사용한 연습

---

## 📌 개념 정리

### 💡 클라이언트 사이드 렌더링 (CSR)이란?

* 페이지가 브라우저에 로드된 후, **브라우저 안에서 데이터를 가져와 렌더링**하는 방식
* React 컴포넌트가 마운트된 후 `useEffect()` 안에서 API 호출

---

## 🔧 필요한 도구

* **React Hooks**

  * `useEffect`: 컴포넌트가 처음 화면에 나타날 때 실행
  * `useState`: 가져온 데이터를 저장
* **fetch()** 또는 **axios**

  * 외부 API와 통신하는 자바스크립트 함수/라이브러리

---

## 🧪 실습 예시: JSONPlaceholder에서 게시글 가져오기

### ✅ 목표

* [https://jsonplaceholder.typicode.com/posts](https://jsonplaceholder.typicode.com/posts) 에서 게시글 가져오기
* 제목 목록을 페이지에 보여주기

---

## 📄 코드 예제: `/pages/posts.tsx`

```tsx
'use client'  // 최신 Next.js app 디렉토리 사용 시 필요

import { useEffect, useState } from 'react'

export default function Posts() {
  const [posts, setPosts] = useState([])           // 글 목록 저장
  const [loading, setLoading] = useState(true)     // 로딩 상태
  const [error, setError] = useState(null)         // 에러 상태

  useEffect(() => {
    const fetchPosts = async () => {
      try {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts')
        if (!res.ok) {
          throw new Error('데이터를 불러오지 못했습니다.')
        }
        const data = await res.json()
        setPosts(data)     // 데이터 저장
      } catch (err) {
        setError(err.message)
      } finally {
        setLoading(false)  // 로딩 끝
      }
    }

    fetchPosts()
  }, []) // 빈 배열: 컴포넌트가 처음 로드될 때 한 번만 실행

  if (loading) return <p>⏳ 로딩 중...</p>
  if (error) return <p>❌ 에러 발생: {error}</p>

  return (
    <div>
      <h1>📋 게시글 목록</h1>
      <ul>
        {posts.map((post: any) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  )
}
```

---

## 🔍 코드 설명

### `useEffect(() => { ... }, [])`

* 컴포넌트가 **브라우저에 처음 그려질 때 한 번만 실행**
* 이 안에서 API 호출을 처리함

---

### `fetch('https://...')`

* 외부 API에 GET 요청을 보냄
* `await res.json()`을 통해 JSON 응답을 자바스크립트 객체로 변환

---

### 상태(state) 3가지

| 변수        | 역할               |
| --------- | ---------------- |
| `posts`   | 받아온 데이터 저장       |
| `loading` | 데이터 불러오는 중 표시 여부 |
| `error`   | 에러 메시지 저장        |

---

## 🧪 추가 실습 예시: 포켓몬 API

### 📄 `/pages/pokemon.tsx`

```tsx
'use client'

import { useEffect, useState } from 'react'

export default function Pokemon() {
  const [data, setData] = useState(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    fetch('https://pokeapi.co/api/v2/pokemon/pikachu')
      .then(res => res.json())
      .then(data => {
        setData(data)
        setLoading(false)
      })
  }, [])

  if (loading) return <p>로딩 중...</p>

  return (
    <div>
      <h1>{data.name.toUpperCase()}</h1>
      <img src={data.sprites.front_default} alt="포켓몬 이미지" />
    </div>
  )
}
```

---

## ❗ 주의할 점

* **useEffect는 브라우저에서만 실행**됨 → `서버에서는 동작 안 함`
* 서버에서 데이터를 먼저 가져오고 싶다면 → 3단계 SSR/SSG에서 배움
* `fetch`가 에러나면 `.ok`를 꼭 확인하거나 `try/catch` 사용해야 함

---

## 🧩 보너스: 상세 페이지 연동

`/posts/[id].tsx` 같은 동적 라우팅을 사용해서 글을 클릭하면 상세 페이지로 이동하는 기능도 연습할 수 있어.
이건 원하면 2단계 확장 실습으로 따로 알려줄게!

---

## 📌 요약표

| 개념                    | 설명                  |
| --------------------- | ------------------- |
| `useEffect()`         | 컴포넌트 마운트 시 실행       |
| `fetch()`             | 외부 API 호출           |
| `useState()`          | 상태 저장               |
| `loading`, `error` 처리 | 사용자 경험 향상           |
| JSONPlaceholder       | 테스트용 API            |
| CSR                   | 브라우저에서 API 호출 후 렌더링 |


