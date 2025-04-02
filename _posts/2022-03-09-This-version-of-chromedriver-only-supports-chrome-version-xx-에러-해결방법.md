---
title: This version of chromedriver only supports chrome version xx 에러 해결방법
date: 2022-03-09 00:19:00 +0900
tags: [chromedriver]
---

# 에러 내용

이전에 만들어둔 크롤링 파일을 오랜만에 실행시키려고 하니,   
chromedriver의 버전이 chrome browser의 버전과 맞지 않아 에러가 발생하였다.
chrome browser는 기본적으로 자동 업데이트를 걸고 있기 때문에 chromedriver가 이보다 버전이 낮게 되어 생긴 문제.

```python
selenium.common.exceptions.SessionNotCreatedException: Message: session not created: This version of ChromeDriver only supports Chrome version 96
Current browser version is 99.0.4844.51 with binary path /Applications/Google Chrome.app/Contents/MacOS/Google Chrome
```

# 기존 chromedriver 버전 확인

```bash
{22-03-08 23:23}P79305:~ minah.kim% which chromedriver
/usr/local/bin/chromedriver
{22-03-08 23:58}P79305:~ minah.kim% /usr/local/bin/chromedriver -v
ChromeDriver 96.0.4664.45 (76e4c1bb2ab4671b8beba3444e61c0f17584b2fc-refs/branch-heads/4664@{#947})
```

현재 버전은 96. chrome 버전에 맞게 업데이트를 해줘야 한다.

# 새 버전의 chromedriver 설치

아래 주소에 접속하여, 99.0.4844.51의 .zip파일을 다운로드 및 unzip 한다.
[chromedriver.chromium.org/downloads](https://chromedriver.chromium.org/downloads)

chromedriver의 바이너리 파일은 아래와 같은 경로를 참조하고 있다.

```bash
{22-03-09 0:06}P79305:~ minah.kim% ll /usr/local/bin/chromedriver
lrwxr-xr-x  1 minah.kim  admin    58B Nov 29 23:17 /usr/local/bin/chromedriver -> /usr/local/Caskroom/chromedriver/96.0.4664.45/chromedriver
```

따라서, 새로운 버전의 폴더를 만들어 주고 이 안에 unzip한 chromedriver파일을 이동시켜 준다.

```bash
{22-03-09 0:04}P79305:/usr/local/Caskroom/chromedriver minah.kim% ll
total 0
drwxr-xr-x@ 3 minah.kim  admin    96B Nov 29 23:17 96.0.4664.45
{22-03-09 0:04}P79305:/usr/local/Caskroom/chromedriver minah.kim% mkdir 99.0.4844.51
{22-03-09 0:04}P79305:/usr/local/Caskroom/chromedriver minah.kim% cd 99.0.4844.51
```

그러면 아래와 같이 두 버전의 chromedriver가 존재하게 된다.

```bash
{22-03-09 0:07}P79305:/usr/local/Caskroom/chromedriver minah.kim% ll *
96.0.4664.45:
total 32416
-rwxrwxrwx@ 1 minah.kim  admin    16M Nov 11 11:02 chromedriver

99.0.4844.51:
total 32536
-rwxr-xr-x@ 1 minah.kim  INTRA\Domain Users    16M Feb 27 06:59 chromedriver
```

기존 chromedriver에 맞게 권한을 777로 변경시켜 주자.

```bash
{22-03-09 0:07}P79305:/usr/local/Caskroom/chromedriver/99.0.4844.51 minah.kim% chmod 777 chromedriver
{22-03-09 0:07}P79305:/usr/local/Caskroom/chromedriver/99.0.4844.51 minah.kim% ll chromedriver
-rwxrwxrwx@ 1 minah.kim  INTRA\Domain Users    16M Feb 27 06:59 chromedriver
```

그리고 바이너리 파일이 99버전의 chromedriver를 바라보도록 심링크를 다시 걸어주자.

```bash
{22-03-09 0:10}P79305:/usr/local/bin minah.kim% rm chromedriver
{22-03-09 0:10}P79305:/usr/local/bin minah.kim% ln -s /usr/local/Caskroom/chromedriver/99.0.4844.51/chromedriver chromedriver
{22-03-09 0:10}P79305:/usr/local/bin minah.kim% ll chromedriver
lrwxr-xr-x  1 minah.kim  admin    58B Mar  9 00:10 chromedriver -> /usr/local/Caskroom/chromedriver/99.0.4844.51/chromedriver
```

그리고 다시 크롤링 파일을 실행시킨다.   
이 때, chromedriver에 대해 신뢰할 수 없는 파일이라고 경고문이 나오는데, Preference > Security & Privacy에서,  
Allow Anyway 버튼을 한 번 눌러주자.    
![image-20220309001207348](/Users/minah.kim/Library/Application Support/typora-user-images/image-20220309001207348.png)

이후 다시 크롤링 파일을 실행시키니 문제없이 실행되었다.

# 보충내용

chromedriver 또한 자동 업데이트를 실행해주는 옵션이 없을까 하여 검색해보니,   
[webdriver-manager](https://yuki.world/python-selenium-chromedriver-auto-update/) 라는 라이브러리를 통해 가능한 것 같다.   
후에 필요할 수도 있으므로 일단 메모.