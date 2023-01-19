---
layout: post
title: "[Web] next.js로 살펴보는 SSR(Server Side Rendering)"
date: 2023-01-19 10:03:38 +0530
categories: Web
---

next.js로 SSR을 이해해보자

# CSR

---

- 장점
  - 유저가 같은 사이트 내에서 url을 이동해서 서버에서 새로운 html을 받지 않고 클라이언트에서 변경된 부분만 업데이트한다.
  - 따라서 화면 깜빡임 없이 앱과 같은 경험으로 웹사이트를 사용할 수 있다.
- 단점
  - 번들링된 js 파일의 크기가 크기 때문에 사용자가 웹사이트에 처음 들어왔을 때 화면이 렌더링되는 것을 보는 데까지 시간이 오래 걸린다.
    - 하지만 이 단점은 **code splitting**으로 어느정도 해결할 수 있다.
    - `code splitting`: 코드를 쪼갠다. **url마다 각각의 번들링된 js 파일을 만들 수 있다**. -> bundle.js의 부담이 적어져 로드 시간이 빨라진다.
- SEO(검색 엔진 최적화) 대응이 어렵다.
  - 국내 검색봇들은 html을 기반으로 요소를 찾기 때문에 빈 html을 내려주는 CSR을 사용하면 불리하다.

### 단점을 극복해보자

사용자가 처음 들어왔을 때 페이지는 서버에서 받아 렌더링하고(SSR, 내용이 모두 채워져있는 html을 받음), 그 뒤에 발생하는 라우팅은 클라이언트 사이드 렌더링(CSR)으로 하면 어떨까?

- SEO 대응이 가능해지고 code splitting을 안 했을 때 CSR 방식보다 사용자가 화면을 보는 타이밍도 빨라진다.
- 이후에 CSR 방식으로 동작하면 유저가 url을 이동해도 페이지 깜빡임 없이 서비스를 사용할 수 있다.

# Next.js

---

SSG(Static Site Generation) 방식으로 동작한다.

### CSR vs SSR vs SSG

- CSR: 웹사이트 진입 시, 비어 있는 html 응답
- SSR: 요청이 들어오면 js를 바로 html로 만들어 응답
- SSG: Build Time에 js를 변환해서 html을 미리 만들어두고, 요청이 들어오면 미리 만들어둔 html 응답

### 예제로 확인하기

크롬 개발자 도구 Network > Docs로 라우팅 처리 했을 때 네트워크 상황을 확인할 수 있다.

# Reference

- [개발화라리 Hwarang](https://www.youtube.com/watch?v=6Ti_A3vMJvk)
