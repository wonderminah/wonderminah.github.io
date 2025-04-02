---
title: GitHub Actions 에러 The job was not started because recent account payments have failed or your spending limit needs to be increased 해결 방법
date: 2025-04-01 18:49:00 +0900
tags: [github, github-action]
---

# 문제 개요

프로덕션 서버에 릴리즈 하는 과정에서 GitHub Action 의 Job 을 실행하는 스텝이 있는데, 아래와 같은 에러가 발생했다.

```
The job was not started because recent account payments have failed or your spending limit needs to be increased. Please check the 'Billing & plans' section in your settings.
```

 로그인한 Account 에 의존하는 문제가 아닐까 싶어, 임시방편으로 다른 팀원의 GitHub Account 로 Job을 실행해보니 웬걸, 해결이 되었다. 

# 발생 경위 조사

이후 조사를 위해 회사 GitHub 관리팀에 문의한 바, 다음과 같았다.

- Spending Limit 은 계약된 Plan 에 따라 다르다.
- 회사가 계약한 Plan 에 따라 월 이용금액 한도가 XXX달러로 지정되어 있다.
- Usage(예: Job 실행시간) 에 따라 이용금액이 환산된다. (따라서 'Job 실행시간'은 월별 고정한도가 있는게 아니라 가변적이다.)
- 회사 Organization 내의 이용이 대상이므로, 그 Organization 안에서의 Usage 가 과금 대상이 된다고 한다.
- Spending Limit 의 확인은 GitHub 관리자만 가능하다.
- GitHub 관리팀에 연락하면 Spending Limit 을 임시로 늘리는 것은 가능하다고 한다.

 

[GitHub 공식 홈페이지](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/managing-your-spending-limit-for-github-actions#about-spending-limits-for-github-actions)에서 Spending Limit 에 조사해본 바, 다음과 같았다.

> GitHub Actions usage is free for standard GitHub-hosted runners in public repositories, and for self-hosted runners

- standard GitHub-hosted runners 의 경우 public repo 에 한해 Usage 가 free
- self-hosted runners 의 경우 Usage 가 free 

릴리즈 중 문제가 일어난 곳은 standard GitHub-hosted runners 의 private repo였다.
public repo 로 전환하지 않는 한, Usage 제약을 피하려면 self-hosted runners 를 고려해야 한다.
인프라 팀에 의하면 self-hosted runners 로써 AWS CodeDeploy 를 이용 가능하다고 하는데,
이제껏 처음 발생한 문제이고 어쩌다 월말에 발생한 문제로 보여, 일단은 두고보기로 했다.
업무에 지장이 생길 정도로 자주 발생한다면 AWS CodeDeploy를 검토하는 것으로.

# 향후 대응 방안

1. 임시방편으로, 다른 GitHub Account 로 로그인하여 다시 시도하고 에러없이 실행이 완료되는지 본다.
2. 1.의 해결 방법이 어렵다면, GitHub 관리팀에 연락하여 Spending Limit 을 일시적으로 늘려주도록 의뢰한다.
3. 문제가 자주 발생한다면, self-hosted runners 를 검토한다.