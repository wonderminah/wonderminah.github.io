---
title: Double dot and Triple dot when using git diff
date: 2022-03-09 10:20:00 +0900
tags: [git]
---

# git diff의 dot 사용 용법

아래와 같이 3가지 방법이 있다.

* 공백 (`git diff MASTER PRIVATE`)
  * 두 개의 dot과 100% 동일하다.
* 두 개의 dot (`git diff..MASTER PRIVATE`)
  * 두 브랜치의 최신 상태를 비교한다.
  * 즉, **private의 변경 내용과 master의 변경 내용이 모두 diff로 출력된다.**
* 세 개의 dot (`git diff...MASTER PRIVATE`)
  * private이 master로부터 처음 갈라지는 지점의 커밋으로부터, private의 최신 커밋의 차이를 비교한다.
  * 즉, **private의 변경 내용만 출력된다.**

master 브랜치와 현재 개발중인 feature 브랜치의 diff를 각각의 사용 용법으로 출력해보면,   
3개의 dot을 사용하는 경우는 파일 수가 더 적은것을 확인할 수 있다. (master의 변경 내용이 포함되지 않았기 때문)

```bash
git diff origin/master origin/feature/itnavi_phase3_ver2 --name-only | wc -l
     114
git diff origin/master..origin/feature/itnavi_phase3_ver2 --name-only | wc -l
     114
git diff origin/master...origin/feature/itnavi_phase3_ver2 --name-only | wc -l
      61
```

# 참고

* [https://matthew-brett.github.io/pydagogue/git_diff_dots.html](https://matthew-brett.github.io/pydagogue/git_diff_dots.html)
* [https://yakst.com/ja/posts/4116](https://yakst.com/ja/posts/4116)