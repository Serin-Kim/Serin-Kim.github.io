---
layout: post
title: "commit 메시지 수정하기 | remote에 올라간 커밋 메시지 수정하기"
date: 2022-12-21 10:30:36 +0530
categories: Git
---

커밋 메시지를 수정해보자

> 깃헙 블로그를 만드는 과정에서 커밋 컨벤션을 변경했다. 이전에는 `git reset HEAD^` 로 커밋을 없애고 새로 작성했는데 이제는 현명한(?) 방법을 써보고자 정리한다.

## 가장 최근의 commit 메시지 수정하기

- `--amend` 옵션을 사용한다.

```
$ git commit --amend -m "새로운 메시지"
```

## 이전 commit 메시지 수정하기

### git rebase

- 해당 commit으로 이동하여 메시지를 수정하고 branch에 merge하는 방식
- `rebase` 명령어로 merge commit이 생성되는 것을 방지해 깔끔한 커밋을 남길 수 있다.

```
$ git rebase -i HEAD~커밋개수
```

- rebase에서 `-i` 옵션을 주면 대화형으로 수행하여 여러 커밋을 한 번에 변경할 수 있다.
- `HEAD~커밋개수`는 최근 commit 중 커밋개수만큼 불러온다는 뜻이다. 10개를 불러오고 싶으면 `HEAD~10`을 입력하면 된다.

### pick을 reword로 변경하기

`HEAD~커밋개수`를 입력하면 다음과 같이 출력된다.

<img width="472" alt="스크린샷 2022-12-19 오전 10 52 18" src="https://user-images.githubusercontent.com/68533016/208823924-a7aefea3-ee34-4d4a-b297-0e566970cc43.png">

- `pick | 커밋 번호 | 커밋 메시지` 형식이 출력된다.
- `i`를 눌러 편집 모드로 전환한 후 수정하고 싶은 커밋의 `pick`을 `reword`로 변경한 후 `esc`와 `:wq`를 눌러 저장하고 편집 모드를 종료한다.

### commit 메시지 수정하기

<img width="522" alt="스크린샷 2022-12-19 오전 10 52 43" src="https://user-images.githubusercontent.com/68533016/208823977-7277b3e4-b361-4f82-83e1-15f03843f056.png">

## remote에 올라간 메시지를 수정하는 경우

```
$ git push -f 브랜치명
```

- 강제 푸시하여 원격에 덮어쓴다.
- 저장소를 로컬에서 작업하고 있는 팀원은 수동으로 로그를 수정해야 하므로 _[GitHub](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message)에서는 권장하지 않는다_.

<img width="758" alt="스크린샷 2022-12-21 오후 1 58 59" src="https://user-images.githubusercontent.com/68533016/208825155-a3bb73db-ef2c-4873-9aad-b07967ae4e47.png">

## Reference

- [https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message)
- [https://jw910911.tistory.com/77](https://jw910911.tistory.com/77)
- [https://xtring-dev.tistory.com/entry/Git-%EC%9D%B4%EB%AF%B8-commit%ED%95%9C-%EB%A9%94%EC%84%B8%EC%A7%80-%EC%88%98%EC%A0%95%ED%95%98%EA%B8%B0-%EB%B0%94%EB%A1%9C-%EC%9D%B4%EC%A0%84%EA%B7%B8-%EC%A0%84%EB%A6%AC%EB%AA%A8%ED%8A%B8-commit](https://xtring-dev.tistory.com/entry/Git-%EC%9D%B4%EB%AF%B8-commit%ED%95%9C-%EB%A9%94%EC%84%B8%EC%A7%80-%EC%88%98%EC%A0%95%ED%95%98%EA%B8%B0-%EB%B0%94%EB%A1%9C-%EC%9D%B4%EC%A0%84%EA%B7%B8-%EC%A0%84%EB%A6%AC%EB%AA%A8%ED%8A%B8-commit)
