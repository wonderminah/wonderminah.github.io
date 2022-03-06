---
title: "파이썬과 파파고를 이용한 영어문장 자동재생 스크립트"
date: 2022-02-07 01:37:00 +0900
tags: [python]
---

# 문제의 발단

일본어 공부에 가장 도움되었던 방법, 반복 리스닝으로 통문장 암기하기.
몇 달 전부터 업무에서 영어 사용 비중이 급격히 늘어나기 시작하면서, 최근에는 영어 공부에도 같은 방식을 이용하고 있다.

일본어 공부 당시에는 드라마를 통해 공부했기에 대사를 녹음하면 됐었는데,
현재는 아래와 같이 화상 영어회화에서 사용하는 교재의 문장들을 재료로 하고 있어, 이를 읽어줄 음성이 필요했다.

![image-20220207000808928](../assets/img/image-20220207000808928.png)

* (필수) 문장을 읽어줄 tts reader가 필요하다. 이 경우, 반복 재생이 가능해야 한다.
* (선택) mp3 파일로 다운로드가 된다면 더욱 좋겠다.

온라인 tts reader는 반복 재생이 불가하거나, mp3 파일 다운로드를 유료 기능으로 제한하고 있었다.
그렇다면 그냥 파파고에 문장을 붙이고 음성을 재생하는걸 파이썬이 반복 수행한다면? 이라는 아이디어로 구현해 보았다.

# 스크립트 구현

```python
import urllib.parse
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

sentences = [
    "Most people today claim to be extremely busy.",
    "But I wonder if they are any busier than people who lived at other times.",
    "Maybe most people generally regard themselves as being busy even if they are not.",
]

driver = webdriver.Chrome()
for sentence in sentences:
    encoded_sentence = urllib.parse.quote(sentence)
    request_url = "https://papago.naver.com/?sk=en&tk=ko&hn=1&st=" + encoded_sentence
    driver.get(request_url)
    time.sleep(3)
    read_tts_button = driver.find_element(By.CSS_SELECTOR, 'button.btn_sound___2H-0Z')
    for idx in range(0, 5):
        read_tts_button.click()
        time.sleep(0.1 * len(sentence))
```

import문과 sentences 변수를 제외하면 10줄로 끝난다.
이제 스크립트를 재생시켜놓고 열심히 받아쓰기&쉐도잉을 해야지.

# 실행결과

<video controls autoplay src="https://wonderminah.github.io/assets/video/video-202202070139.mov"></video>

# 메모

음성재생 버튼을 눌렀을 때 /apis/tts로 요청되는 Request URL에 접속하면 mp3 저장이 가능하다는 것까지는 알았는데,
출퇴근을 안해 당분간은 집에서만 들을 것 같으므로 일단 메모해두고 SKIP.

![image-20220207003959553](../assets/img/image-20220207003959553.png)

![image-20220207003732081](../assets/img/image-20220207003732081.png)
