---
title: "How to change author of pushed commit"
date: 2022-04-07 22:22:34 +0900
tags: [git]
---

회사 컴퓨터로 작업을 하다보니 git의 global로 설정되어 있는 username과 useremail이 개인 프로젝트에도 설정된 채로 커밋이 올라가 버린 것을 발견했다. 이를 바꾸는 과정을 포스팅하도록 하자.

![image-20220407222326107](../assets/img/image-20220407222326107.png)

```bash
commit ff5bbbd0e735593c4a17502a097887a63477fb36 (HEAD -> master)
Author: Kim, Minah | Minah | MSD <minah.kim@rakuten.com>
Date:   Wed Mar 16 00:57:11 2022 +0900

    Upload dataset and example sourcecode

commit b71f6f46b70f48eb51f26aa5f760988f11147712 (origin/master)
Author: Kim, Minah | Minah | MSD <minah.kim@rakuten.com>
Date:   Wed Mar 16 00:56:31 2022 +0900

    Initial Commit
```

# 개인 프로젝트에 git config --local로 유저 재설정

해당 프로젝트에만 적용되도록 --local 옵션을 기재한다.

```bash
git config --local user.name "wonderminah"
git config --local user.email "minah.kim@rakuten.com"
```

# 변경할 커밋 지정

```bash
$ git rebase -i HEAD~1
```

vi가 열리면서 아래와 같은 결과가 나오는데, i를 눌러 insert 모드로 들어간 다음 pick을 edit으로 변경하고 :wq로 저장해준다.

```bash
pick ff5bbbd Upload dataset and example sourcecode
```

그럼 아래와 같은 메시지가 출력된다.

```bash
Updating files: 100% (19/19), done.
Stopped at ff5bbbd...  Upload dataset and example sourcecode
You can amend the commit now, with

  git commit --amend

Once you are satisfied with your changes, run

  git rebase --continue
```

# 변경할 내용 입력

아래 커맨드와 같이 `--author="아이디 <이메일>"`의 형태로 author를 변경한다.

```bash
$ git commit --amend --author="wonderminah <kimma1205@gmail.com>"
```

# 변경 완료 후 push

```bash
$ git rebase --continue
Successfully rebased and updated refs/heads/master.
$ git push
Enumerating objects: 27, done.
Counting objects: 100% (27/27), done.
Delta compression using up to 16 threads
Compressing objects: 100% (26/26), done.
Writing objects: 100% (26/26), 78.20 MiB | 3.68 MiB/s, done.
Total 26 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
remote: error: Trace: 89affffda9574b140c968831466a7aa2c752fccb13cda95d2a7a2438f3d04f1f
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File dataset/상가상권정보/상가업소정보_201912_01.csv is 252.65 MB; this exceeds GitHub's file size limit of 100.00 MB
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
To https://github.com/wonderminah/open-data-analysis-basic.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'https://github.com/wonderminah/open-data-analysis-basic.git'
```

용량 초과로 push가 안 된다는 메시지는 처음 보는데 .. 이건 별도로 해결하도록 하자.