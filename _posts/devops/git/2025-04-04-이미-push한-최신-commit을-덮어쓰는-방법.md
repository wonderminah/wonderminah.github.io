---
title: 이미 push한 최신 commit을 덮어쓰는 방법
date: 2025-04-04 01:57:00 +0900
tags: [git]
---

블로그 포스팅을 정리하고 git push를 하고나면, 아차 깜빡했다 싶을때가 있다. 예를 들면 블로그 포스팅에 categories를 잘못 지정했다거나. 그런데 그런 수정사항 만으로 commit을 한 개 더 쌓기가 싫다. 기왕이면 이미 push해버린 commit을 취소하고 새로운 commit으로 덮어써서 깔끔하게 commit 목록을 정리하고 싶다. 이럴 때 쓸 수 있는 git command를 정리한다. (당연하게 외우고 있던건데 git좀 안만진지 시간좀 됐다고 그새 잊어버렸다.)

# 기존의 상태

![image-20250404005725107](../assets/img/image-20250404005725107.png)

최신 commit 의 ID는 `1247a00`이다. 이것을 새로운 커밋으로 덮어쓸 것이다.

# 커밋 덮어쓰기 (git reset HEAD~1)

결론부터 이야기하면 `git reset HEAD~1` 와 `git push -f` 가 끝이다.

```shell
# 포스트 파일에서 categories 를 수정한다.
vi _posts/blog/jekyll/2025-04-04-Jekyll-블로그를-로컬에서-실행하기.md

# 커밋의 위치를 하나 되돌린다.
git reset HEAD~1

# 수정한 포스트 파일을 add하고, 다시 commit 메시지를 작성한다.
git add _posts/blog/jekyll/2025-04-04-Jekyll-블로그를-로컬에서-실행하기.md
git commit -m "포스트 업로드 - Jekyll 블로그에서 Categories를 이용하여 메뉴별로 포스트 분류하기"

# -f 옵션을 붙여 강제로 푸시한다.
git push -f
```

![image-20250404005923863](../assets/img/image-20250404005923863.png)

이전 ID `1247a00` 은 사라지고, 최신 commit 의 ID는 `432206b` 로 확인되는 걸 볼 수 있다.

# 주의사항

리모트 리포지토리의 commit 을 강제로 지우는 행위이다.
혼자서 작업하는 repository 라면 상관없지만, 협업할때는 다른 사람의 commit 에 손대지 않도록 주의하도록 하자.