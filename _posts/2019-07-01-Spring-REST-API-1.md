---
title: "Spring기반 REST API - 1"
date: 2019-03-01 14:23:28 -0400
categories: spring
---

ch1. REST API 및 프로젝트 소개
========================

### REST API

- API
    - Application Programming Interface

- REST
    - REpresentational State Transfer
    - 인터넷 상의 시스템 간의 상호 운용성(interoperability)을 제공하는 방법중 하나
    - 시스템 제각각의 독립적인 진화를 보장하기 위한 방법
    - REST API: REST 아키텍처 스타일을 따르는 API

- REST 아키텍처 스타일 (발표 영상 11분)
    - Client-Server
    - Stateless
    - Cache
    - Uniform Interface
    - Layered System
    - Code-On-Demand (optional)

- Uniform Interface ([발표 영상](https://www.youtube.com/watch?v=RP_f5dMoHFc) 11분 40초)
    - Identification of resources
    - manipulation of resources through represenations
    - self-descrive messages
    - hypermisa as the engine of appliaction state (HATEOAS)


- Self-descriptive message
    - 메시지 스스로 메시지에 대한 설명이 가능해야 한다.
    - 서버가 변해서 메시지가 변해도 클라이언트는 그 메시지를 보고 해석이 가능하다.
    - 확장 가능한 커뮤니케이션
- HATEOAS
    - 하이퍼미디어(링크)를 통해 애플리케이션 상태 변화가 가능해야 한다.
    - 링크 정보를 동적으로 바꿀 수 있다. (Versioning 할 필요 없이!)

- Self-descriptive message 해결 방법 
    - 방법 1: 미디어 타입을 정의하고 IANA에 등록하고 그 미디어 타입을 리소스 리턴할 때 Content-Type으로 사용한다.
    - 방법 2: profile 링크 헤더를 추가한다. (발표 영상 41분 50초)
        - 브라우저들이 아직 스팩 지원을 잘 안해
        - 대안으로 HAL의 링크 데이터에 profile 링크 추가

- HATEOAS 해결 방법 
    - 방법1: 데이터에 링크 제공
        - 링크를 어떻게 정의할 것인가? HAL
    - 방법2: 링크 헤더나 Location을 제공