# ✅ 1단계: Next.js 기본 구조 이해

Next.js는 React 위에 만들어진 프레임워크로, **페이지 기반 라우팅**, **서버 사이드 렌더링**, **API 라우트** 기능까지 포함된 강력한 도구야.

---

## 📦 1-1. Next.js 설치

### 🛠️ 설치 방법

```bash
npx create-next-app@latest my-next-app
cd my-next-app
npm run dev
```

* `npx create-next-app@latest`: 최신 버전의 Next.js 프로젝트 생성
* `npm run dev`: 개발 서버 실행 → 브라우저에서 `http://localhost:3000`으로 접속

---

## 📂 1-2. 폴더 구조 이해

```
my-next-app/
├── app/         ← 최신 버전에서는 이 폴더 사용 가능 (App Router 방식)
├── pages/       ← 가장 기본적인 라우팅을 담당하는 폴더
│   ├── index.tsx     → / 경로
│   ├── about.tsx     → /about 경로
│   └── api/          → API 라우트 폴더
├── public/      ← 이미지, favicon 등 정적 파일 넣는 곳
├── styles/      ← CSS 파일들
├── package.json ← 프로젝트 설정
```

### ✅ `pages` 폴더

* `pages/index.tsx` → 홈페이지 (`/`)
* `pages/about.tsx` → 소개 페이지 (`/about`)
* 이 폴더 안의 파일명 = URL 경로!

---

## 🌐 1-3. 라우팅 방식

Next.js는 **파일 기반 라우팅**을 사용해.

### 예시:

* `pages/index.tsx` → `http://localhost:3000/`
* `pages/about.tsx` → `http://localhost:3000/about`
* `pages/posts/[id].tsx` → 동적 라우팅 (예: `/posts/1`, `/posts/abc`)

라우팅을 위해 따로 설정할 필요 없어! 파일만 잘 만들면 됨.

---

## 🧩 1-4. 컴포넌트 기본 구조

Next.js도 결국 React니까 기본적인 컴포넌트 작성법은 같아.

### 📄 `pages/index.tsx`

```tsx
export default function Home() {
  return (
    <div>
      <h1>홈페이지입니다</h1>
    </div>
  );
}
```

* 함수형 컴포넌트를 `export default`로 내보내야 페이지로 인식됨

---

## 🧪 1-5. 실습 예시 1 – 홈과 소개 페이지 만들기

### 📄 `pages/index.tsx`

```tsx
export default function Home() {
  return (
    <div>
      <h1>홈 페이지</h1>
      <p>여기는 메인 페이지입니다.</p>
    </div>
  );
}
```

### 📄 `pages/about.tsx`

```tsx
export default function About() {
  return (
    <div>
      <h1>소개 페이지</h1>
      <p>이 페이지는 저를 소개하는 곳입니다.</p>
    </div>
  );
}
```

📌 브라우저에서 `/`와 `/about`으로 각각 이동해서 확인해보세요.

---

## 🔘 1-6. 실습 예시 2 – 버튼 클릭 시 텍스트 변경

### 📄 `pages/index.tsx`

```tsx
'use client' // 최신 Next.js에서 client 컴포넌트로 지정할 때 필요 (app 디렉토리 기반인 경우)

import { useState } from 'react'

export default function Home() {
  const [text, setText] = useState('처음 문장')

  return (
    <div>
      <h1>홈 페이지</h1>
      <p>{text}</p>
      <button onClick={() => setText('버튼이 클릭되었습니다!')}>
        클릭하기
      </button>
    </div>
  )
}
```

### 💡 핵심 개념

* `useState`: 컴포넌트 내 상태(state) 저장
* 버튼 클릭 → 상태 변경 → 화면 자동 업데이트

---

## 📌 마무리 요약

| 항목         | 설명                                |
| ---------- | --------------------------------- |
| Next.js 설치 | `npx create-next-app`으로 시작        |
| 폴더 구조      | `pages`, `public`, `styles` 주요 폴더 |
| 라우팅        | 파일 기반 자동 라우팅                      |
| 컴포넌트       | React 함수형 컴포넌트 사용                 |
| 실습         | 페이지 생성, 버튼 클릭 상태 변경               |

