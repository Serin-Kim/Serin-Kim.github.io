---
layout: post
title: "GitHub 블로그 만들기 - Jekyll theme 적용하는 법 | Jekyll theme could not be found 오류 | chrome 에서 Jekyll css 깨지는 오류"
date: 2022-12-19 10:03:36 +0530
categories: Git TroubleShooting Blog
---

GitHub 블로그를 만들어보자

# # Jekyll 테마 적용하는 법

## 1. 새로운 Repository 생성하기

- `사용자이름/github.io` 으로 Repository name을 설정한다.

- 로컬에 클론한다.

## 2. 블로그 테마 선택하기

- 원하는 Jekyll 테마를 고른다.

  - 깔끔하고 다크 모드로 전환이 가능한 [plainwhite](https://github.com/samarsault/plainwhite-jekyll) 테마를 선택했다.
  - 카테고리, 댓글, excerpt 등 일부 기능은 커스텀하기로 결정했다.

- 해당 저장소에서 코드를 다운 받아 전체 복사를 한 후, `1번` 에서 클론해온 `사용자이름/github.io` 폴더에 붙여 넣는다.
  - 중복 파일은 덮어쓰면 된다.

## 3. bundle 설치

```
$ bundle install
```

- Jekyll 은 Ruby 환경에서 돌아간다. Ruby가 설치 되어있지 않다면 [공식문서](https://jekyllrb.com/docs/) 를 참고하면 된다.

## 4. Jekyll 서버 실행

```
$ bundle exec jekyll serve
```

- Jekyll 서버가 로컬에서 실행된다. `http://127.0.0.1:4000/` 에서 확인할 수 있다.

## 5. 원격 저장소에 push

<img width="657" alt="스크린샷 2022-12-19 오후 8 17 39" src="https://user-images.githubusercontent.com/68533016/208414563-2b0dfa48-5438-4587-bd50-11710b712271.png">

- 빌드와 deploy 에러가 나지 않는다면 ✅ 표시가 뜬다.
- 주소창에 `사용자이름/github.io` 를 입력하면 배포된 블로그를 확인할 수 있다.

## # Jekyll theme could not be found 오류

> [블로그](https://zeddios.tistory.com/1223) 를 똑같이 따라했는데 `로컬에서는 테마가 적용되지만 push했을 때 git에서 빌드에 실패하는 문제`가 발생했다.

<img width="1482" alt="스크린샷 2022-12-19 오전 12 29 57" src="https://user-images.githubusercontent.com/68533016/208413961-25316e6d-40ad-4ef7-b45c-e9acfa6a1c1e.png">
<img width="1490" alt="스크린샷 2022-12-19 오전 12 30 08" src="https://user-images.githubusercontent.com/68533016/208413965-ef3e9392-7519-4a94-b1b3-203a97abe776.png">

### 해결 방법

1. `Gemfile` 에 plainwhite 추가

```
gem "plainwhite"
```

2. `_config.yml` 에 theme 제거 (주석 처리) 후 remote_theme 추가

```
remote_theme: samarsault/plainwhite-jekyll
# theme: plainwhite
```

### 트러블 슈팅에 대한 한 마디

며칠 동안 헤맸는데 stackoverflow 에서 `테마는 잘못이 없다. 셋팅 과정에서 오류가 났을 것이다`라는 코멘트를 봤다. 그리고 정말로 테마는 잘못이 없었다 ..ㅎㅎ 깃헙 블로그를 처음 쓰는 사람들은 gem이나 liquid 에 익숙하지 않아서 시행착오가 많을 것 같다. `bundle`과 `jekyll` 이 어떤 동작을 하는지 파악하는 과정이 문제 해결에 도움이 됐던 것 같다. 지킬 공식 문서를 참고하자!

# # 크롬 브라우저에서 css가 적용되지 않는 오류

> 사파리, 모바일에서는 괜찮았지만 크롬에서 열면 레이아웃이 적용되지 않는 문제가 발생했다.

<img width="400" alt="스크린샷 2022-12-19 오전 10 34 03" src="https://user-images.githubusercontent.com/68533016/208416280-93a1b082-dcc7-4b32-941d-541e8c241d78.png">

### 해결 방법

- css가 캐싱되어 발생한 문제이다.
- 개발자 도구를 연 상태에서 크롬의 새로고침 버튼 우클릭 > `캐시 비우기 및 강력 새로고침` 클릭한다.

### 트러블 슈팅에 대한 한 마디

나의 경우, 캐시를 비워도 새로고침하면 레이아웃이 깨진 상태로 돌아왔다. 결국에 크롬을 재설치 해서 문제를 해결했다. 근본적인 원인을 해결하지 못한 것 같아서 아쉽다.

## Reference

- https://pages.github.com/
- https://jekyllrb.com/
- https://zeddios.tistory.com/1223
- https://github.com/samarsault/plainwhite-jekyll
