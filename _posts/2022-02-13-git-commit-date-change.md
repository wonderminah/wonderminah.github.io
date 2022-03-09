---
title: "How to change git commit datetime"
date: 2022-02-17 01:17:00 +0900
tags: [git]
---

# git log

```bash
git log
```

```bash
commit a7b5e2e982e63c37584418c9564cd618c2a7362d
Author: Kim, Minah
Date:   Sun Feb 13 23:04:04 2022 +0900

    キーワードの検索結果数の表示を削除

commit ca7368bac9c2214f95b5e0398de22409784df6d3
Author: Kim, Minah
Date:   Sun Feb 13 22:59:35 2022 +0900

    Add validation

commit e5e5b5edad276ac1e45357adec1a053cdf330edf
Merge: df733147 2378277c
Author: Kim, Minah
Date:   Sun Feb 13 22:47:04 2022 +0900

    Merge branch 'feature/itnavi_phase3_ver2' into private/itnavi_phase3_ver2/dev_minah
```

ca7368ba 커밋을 고치고 싶다고 가정하자.
이 경우, 그 이전의 커밋 e5e5b5ed을 복사하여 아래와 같이 실행한다.

# git rebase -i {커밋}, edit

```bash
git rebase -i e5e5b5edad276ac1e45357adec1a053cdf330edf
```

실행하면 아래와 같이, e5e5b5ed 커밋 이후의 커밋 목록이 화면에 표시된다.

```bash
pick ca7368ba Add validation
pick e1f42c6f キーワードの検索結果数の表示を削除
pick 19a2c904 並び替え処理
pick 3b503314 id_ indexを0から始まるように変更
pick ca911123 Modify validation for 'keyword'

# Rebase ca7368ba..ca911123 onto 3b503314 (5 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

i를 입력하여 vim의 INSERT모드로 들어간 후, 아래와 같이 고치고 싶은 커밋 ca7368ba 좌측의 'pick'을 'edit'으로 고친다.

```bash
edit ca7368ba Add validation
```

:wq를 입력하여 저장 후 vim을 나간다. 그럼 아래와 같은 상황이 된다.

```bash
Stopped at ca7368ba...  Add validation
You can amend the commit now, with

  git commit --amend

Once you are satisfied with your changes, run

  git rebase --continue
```

# git commit --amend --date={일시}

아래와 같이 수정하고 싶은 일시를 지정하여 커밋을 수정한다.

```bash
git commit --amend --no-edit --date="FEB 10 19:21:23 2022 +0000"
[detached HEAD 5666fe96] Add validation
 Date: Thu Feb 10 19:21:23 2022 +0000
 1 file changed, 30 insertions(+)
```

수정 후 git log를 입력하여 확인해 보면, 아래와 같이 지정한 일시로 변경된 것을 확인할 수 있다.

```bash
commit 5666fe9643b2a77f787a5eae762aec29967787cd (HEAD)
Author: Kim, Minah | Minah | MSD <minah.kim@rakuten.com>
Date:   Thu Feb 10 19:21:23 2022 +0000

    Add validation
```

# git rebase --continue

git rebase --continue를 실행하여, 수정을 완료한다.

```bash
git rebase --continue
Successfully rebased and updated refs/heads/private/itnavi_phase3_ver2/dev_minah.
```

