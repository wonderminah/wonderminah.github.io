---
title: "About OAuth and OpenID Connect"
date: 2023-01-09 01:33:00 +0900
tags: [OAuth, OpenID]
---

# About OAuth and OpenID Connect

## OAuth

異なるシステム間でデータや機能へのアクセス権限の許可を行う仕組み
[一番分かりやすい OAuth の説明](https://qiita.com/TakahikoKawasaki/items/e37caf50776e00e733be)
https://ja.wikipedia.org/wiki/OAuth

* リソースオーナー：リソースオーナーが人間である場合は、リソースオーナーの事を**エンドユーザー**ともいう。 
* リソースサーバー
* クライアント
* 許容サーバー

![image-20221017225252067](/Users/minah.kim/Library/Application Support/typora-user-images/image-20221017225252067.png)

![image-20221017221336679](/Users/minah.kim/Library/Application Support/typora-user-images/image-20221017221336679.png)

https://developers.line.biz/ja/docs/line-login/integrate-line-login/#login-flow

## About OpenID Connect

[Next.js 소셜로그인 0) 시작](https://velog.io/@cloud_oort/Next.js-%EC%86%8C%EC%85%9C%EB%A1%9C%EA%B7%B8%EC%9D%B8-0%EC%8B%9C%EC%9E%91) << 설명 아주 잘 나와있음.

※ OpenID Connect？
[一番分かりやすい OpenID Connect の説明](https://qiita.com/TakahikoKawasaki/items/498ca08bbfcc341691fe)

※ OAuthとOpenIDの違い？
하지만 둘은 목적에서 차이를 보인다. 
**OpenID는 인증(Authentication) 자체에 목적**을 두고 있는 반면 
**OAuth**는 인증 후 리소스 또는 API를 사용할 권한을 갖는 다는 것에 목적이 있다. 
즉, **허가(Authorization)**의 목적이라는 것이다. (Source: [Naver D2](https://d2.naver.com/helloworld/24942))

- OpenID Connect: 사용자 인증 및 사용자 정보 제공 (id token)
- OAuth: 권한 부여 (access token) - 페이스북 posting 권한, 유저 profile view 권한 등
  (일시적으로 권한을 허가해 준 토큰일 뿐, 사용자에 대한 정보를 담고있지 않음)

OAuth 2.0은 Access Token을 발급 받고 그 Access Token을 통해서 리소스에 접근하기 위해 사용된다.
반면에 OpenID Connect는 ID Token을 발급 받고 그 ID Token으로부터 사용자 식별 정보를 얻기 위해서 사용된다.

**OAuth 2.0:** 예를 들어 새로운 애플리케이션에 가입하면서 Facebook이나 휴대전화 연락처를 통해 새로운 연락처를 자동으로 제공하는 데 동의했다면 OAuth 2.0을 사용했을 가능성이 높습니다. 이 표준은 안전한 위임 액세스를 제공하기 때문입니다. 다시 말해서 애플리케이션이 자격 증명을 공유하지 않고도 사용자를 대신해 서버에서 리소스에 액세스할 수 있습니다. 이것이 가능한 이유는 [아이덴티티 공급업체(IdP)](https://www.okta.com/identity-101/why-your-company-needs-an-identity-provider/)가 사용자의 승인을 받아 타사 애플리케이션에 토큰을 발행할 수 있기 때문입니다.

**OpenID Connect:** Google을 사용해 YouTube 등의 애플리케이션에 로그인하거나, Facebook을 사용해 온라인 쇼핑 카트에 로그인한다면 이러한 인증 옵션에 대해 잘 알고 있는 셈입니다. OpenID Connect는 사용자 인증에 사용되는 개방형 표준입니다. IdP가 이 표준을 사용하는 이유는 사용자가 IdP에 로그인한 후 다시 로그인하거나 로그인 정보를 공유하지 않고도 다른 웹사이트와 앱에 액세스할 수 있기 때문입니다. 

OpenID Connect 1.0은 OAuth 2.0 프로토콜 위에 있는 간단한 ID 계층이다.
이를 통해 클라이언트는 REST와 유사한 방식으로 최종 사용자의 신원과 기본적인 프로필 정보를 얻을 수 있다.