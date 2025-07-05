# 🛠️ 3단계. 서버 사이드 API 호출 (SSR, SSG)

브라우저가 아닌 **Next.js 서버가 먼저 API를 호출**해서 데이터를 받아온 후, **페이지에 props로 전달**하는 방식이야.
브라우저가 열리기 전에 데이터를 준비해줄 수 있어서 **초기 로딩 속도가 빠르고**, **SEO에도 유리**해.

---

## ✅ 두 가지 방식 요약

| 구분               | SSR (`getServerSideProps`) | SSG (`getStaticProps`) |
| ---------------- | -------------------------- | ---------------------- |
| 실행 시점            | **요청 시마다** 서버에서 실행         | **빌드 시 1회만** 실행        |
| 데이터 최신성          | 항상 최신                      | 고정됨                    |
| 속도               | 느릴 수 있음                    | 빠름                     |
| 브라우저에서 fetch 필요? | ❌ 아님                       | ❌ 아님                   |
| 사용 예시            | 실시간 뉴스, 유저별 페이지            | 정적 블로그, 공지사항           |

---

## 📦 SSR 예제 – 뉴스 목록 페이지

```tsx
// pages/news.tsx

export default function NewsPage({ articles }) {
  return (
    <div>
      <h1>뉴스 목록</h1>
      <ul>
        {articles.map(article => (
          <li key={article.id}>{article.title}</li>
        ))}
      </ul>
    </div>
  )
}

export async function getServerSideProps() {
  const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  const data = await res.json()

  return {
    props: {
      articles: data.slice(0, 10),
    },
  }
}
```

* 페이지 요청 시마다 서버에서 API 호출
* 응답된 데이터를 `props`로 넘겨줌

---

## 🗂️ SSG 예제 – 날짜 정보 페이지

```tsx
// pages/info.tsx

export default function InfoPage({ data }) {
  return (
    <div>
      <h1>오늘의 정보</h1>
      <p>{data}</p>
    </div>
  )
}

export async function getStaticProps() {
  const today = new Date().toISOString()

  return {
    props: {
      data: `이 페이지는 빌드 시점의 날짜입니다: ${today}`,
    },
  }
}
```

* 빌드 시점에 한 번만 실행됨
* 정적 HTML로 만들어져 매우 빠름

---

## 🧠 정리 요약

* ✅ `getServerSideProps` → 요청 시마다 서버가 API 호출 → **실시간 데이터에 적합**
* ✅ `getStaticProps` → 빌드 시 1회만 API 호출 → **변하지 않는 정보에 적합**
* ❌ `useEffect(fetch)`는 **브라우저에서만 실행**, 서버에선 안 됨

---

## 🎯 언제 어떤 걸 써야 할까?

| 상황                         | 추천 방식 |
| -------------------------- | ----- |
| 로그인된 사용자에 따라 다른 데이터 보여줄 때  | SSR   |
| 실시간 뉴스, 주식 정보 등 최신 데이터 필요  | SSR   |
| 회사 소개, 제품 페이지처럼 잘 안 바뀌는 정보 | SSG   |
| 블로그 글처럼 한 번 쓰고 오래 보여주는 데이터 | SSG   |

