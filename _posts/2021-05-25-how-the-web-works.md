---
title:  "웹 동작 원리"
excerpt: "naver.com 으로 웹 화면으로 출력되기까지."

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2021-05-25
---

브라우저에 naver.com 을 입력하고 우리가 사용하는 네이버 서비스를 볼 때까지의 과정을 살펴보자.

## 1. 도메인 네임으로 IP 주소를 얻는다.

가장 먼저 호스트 파일을 참조하여 해당 도메인 주소의 정보가 있는지 확인 후 없다면  
**DNS 프로토콜**을 사용해 우리가 입력한 naver.com 으로 네이버 웹 서버의 IP를 확인한다. 

> ### DNS 프로토콜

![](https://user-images.githubusercontent.com/71869837/119443504-afdfef80-bd64-11eb-9cf2-aefaf8a1876b.png)

1. 웹 브라우저가 로컬 DNS 서버에 naver.com 을 질의한다.
1. 로컬 DNS 서버는 naver.com 을 Root DNS 에게 질의한다. Root DNS는 . 이후의 com 을 인식한 후 com 을 관리하는 최상위 DNS 서버 ip 를 응답한다.
1. 로컬 DNS는 최상위 DNS 서버에게 naver.com 을 질의한다. 최상위 DNS 서버는 naver.com 을 관리하는 책임 DNS 서버의 ip 주소를 응답한다.
1. 로컬 DNS는 책임 DNS 서버에게 naver.com 을 질의한다. 책임 DNS 서버는 해당 웹 서버의 ip 를 응답한다.

> ### DNS 캐싱

- 로컬 DNS 서버는 응답을 받을 때마다 DNS정보를 저장한다.  
이때 브라우저로부터 같은 질의가 들어온다면 저장된 ip를 응답하게 된다.

## 2. http 요청 메세지를 웹서버에 전달 

http 프로토콜을 사용하여 http 요청 메세지를 생성한 후 TCP 프로토콜을 사용하여 해당 웹서버에 전송한다.

http 프로토콜 진행 시 **HSTS** 리스트를 확인 후 https 프로토콜 진행여부를 확인한다.

> ### HSTS

보안을 강회시킬 목적으로 웹 브라우저와 웹 서버의 통신에서 강제적으로 https 프로코콜을 사용하는 기능.

https 란 통신 도중 정보가 제3자에게 노출되지 않도록 통신 내용을 SSL/TLS 방식으로 암호화시켜 통신하는 프로토콜이다.

## 3. 웹서버는 전달받은 요청에 맞는 데이터로 http 응답 메세지를 전달

## 4. 응답 메세지의 데이터가 브라우저의 의해 출력되어 사용자가 웹페이지 확인