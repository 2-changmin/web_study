# 🧩 4단계. API 라우트 – Next.js에서 자체 API 만들기

Next.js는 단순히 프론트엔드 프레임워크가 아니라, **API 서버 역할도 가능**해.
`/pages/api/` 폴더에 파일을 만들면, 그것이 바로 **백엔드 API 엔드포인트**가 돼.

---

## ✅ 핵심 개념

| 개념      | 설명                                             |
| ------- | ---------------------------------------------- |
| API 라우트 | `/pages/api/파일.ts` 형태로 만든 파일이 HTTP API로 작동함    |
| 실행 위치   | **브라우저가 아닌 서버에서 실행**됨                          |
| 사용 목적   | 클라이언트 fetch 요청 처리, 데이터 반환, POST 입력 받기 등        |
| 주요 객체   | `req`(요청), `res`(응답) – Node.js의 HTTP 처리 방식과 유사 |

---

## 📁 폴더 구조 예시

```
pages/
├── index.tsx
├── test.tsx
└── api/
    ├── hello.ts       → /api/hello
    ├── time.ts        → /api/time
    └── echo.ts        → /api/echo
```

---

## 📄 예제 1: 기본 API (GET)

```ts
// pages/api/hello.ts

import { NextApiRequest, NextApiResponse } from 'next'

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ message: '안녕하세요! 이것은 Next.js API입니다.' })
}
```

📍 접속 주소: `/api/hello`
📍 응답 결과: `{ "message": "안녕하세요! ..." }`

---

## 📄 예제 2: 현재 시간 반환 API

```ts
// pages/api/time.ts

export default function handler(req, res) {
  const now = new Date().toLocaleString()
  res.status(200).json({ time: now })
}
```

📍 접속 주소: `/api/time`
📍 응답 결과: `{ "time": "2025. 7. 6. 오후 3:00:00" }`

---

## 📄 예제 3: POST 요청 처리 (Echo API)

```ts
// pages/api/echo.ts

export default function handler(req, res) {
  if (req.method === 'POST') {
    const { message } = req.body
    res.status(200).json({ echo: `당신이 보낸 메시지: ${message}` })
  } else {
    res.status(405).json({ error: '허용되지 않은 메서드입니다.' })
  }
}
```

📍 요청 예시:

```ts
fetch('/api/echo', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ message: '안녕' })
})
```

📍 응답 결과: `{ "echo": "당신이 보낸 메시지: 안녕" }`

---

## 🧪 클라이언트에서 API 호출하기 예제

```tsx
// pages/test.tsx

'use client'

import { useEffect, useState } from 'react'

export default function TestPage() {
  const [time, setTime] = useState('')

  useEffect(() => {
    fetch('/api/time')
      .then(res => res.json())
      .then(data => setTime(data.time))
  }, [])

  return (
    <div>
      <h1>서버 현재 시간</h1>
      <p>{time}</p>
    </div>
  )
}
```

---

## ✅ 요약

| 항목         | 내용                                     |
| ---------- | -------------------------------------- |
| API 생성 위치  | `/pages/api/파일명.ts`                    |
| 실행 환경      | 항상 서버에서 실행                             |
| GET 요청 처리  | 기본 JSON 반환                             |
| POST 요청 처리 | `req.method === 'POST'`, `req.body` 활용 |
| 클라이언트에서 호출 | `fetch('/api/hello')` 등으로 호출 가능        |

---

## 🔧 실습 아이디어

| 이름              | 설명                         |
| --------------- | -------------------------- |
| `/api/time`     | 현재 시간 반환                   |
| `/api/echo`     | 사용자 메시지 그대로 응답             |
| `/api/messages` | POST로 받은 메시지 저장 (임시 메모리 등) |
