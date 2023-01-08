---
title: "About Web API"
date: 2023-01-09 01:31:00 +0900
tags: [Web]
---



# About Web API

※ Wep APIとは
Application Programming Interface
プログラムの機能の一部を別のプログラム上で利用できるように共有する仕組み

※ REST API
Representational State Transfer API

이처럼 REST API 방법을 사용하면 **주소와 메서드만 보고 요청의 내용을 알아볼 수 있다는 장점**이 있다. 그래서 개발자간의 소통도 쉽고 개발 시 혼선도 덜 빚어진다고 한다.

- Representational →具象化された
- State →状態の
- Transfer →転送

REST アーキテクチャスタイルの制約に従い、RESTful Web サービスとの対話を可能にする
RESTと呼ばれる設計原則に従って策定されたもの
웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일입니다. 구체적으로는 HTTP URI를 통해 어떤 자원인지 명시하고, HTTP Method(GET, POST, PUT, PATCH, DELETE)를 통해 해당 자원을 처리하도록 설계된 것입니다.

![image-20221017213505452](/Users/minah.kim/Library/Application Support/typora-user-images/image-20221017213505452.png)

* 자원 Resource

  * 모든 자원에는 고유한 ID가 존재하고, 이 자원은 서버에 존재한다. REST는 자원에 접근할 때 URI(Uniform Resource Identifier)를 이용한다. 여기서 URI는 자원의 위치를 나타내는 일종의 식별자이다. 

    Ex).../board/article/{articleid} -> board 아래 article 아래 {ariticleid} 자원 

    - 동사보다는 명사를, 대문자보다는 소문자
    - 자료에 따라 단수 명사, 복수 명사 구분

* 메서드 Method

  * REST는 기본적으로 HTTP 메서드를 사용한다. 그 종류에는 GET, POST, PUT, DELETE 등이 존재하고, 각각 다음과 같은 역할을 한다. 
    - GET : 해당 리소스를 조회한다. 
    - POST : 해당 리소스를 생성한다
    - PUT : 해당 리소스를 수정한다.
    - DELETE : 해당 리소스를 삭제한다. 
  * URI에 HTTP Method가 들어가면 안됩니다.
  * URI에 행위에 대한 동사 표현이 들어가면 안됩니다.
  * 경로 부분 중 변하는 부분은 유일한 값으로 대체

* 메시지 Message

  * 메시지는 HTTP header, body, 응답 상태 코드 등으로 구성되어 있다. 간단하게 설명하자면 header에는 body에 어떤 형식으로 데이터가 담겼는지 표시하고, body는 자원에 대한 정보를 JSON, XML 등으로 전달한다. 응답 상태 코드는 200~500 사이의 숫자로 클라이언트의 요청에 대한 상태를 나타내 준다.