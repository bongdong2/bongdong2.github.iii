---
title: "springboot & AWS - Travis CI 배포 자동화"
date: 2020-01-11 10:03:00 -0400
categories: spring
---

코드가 푸쉬되면 자동으로 배포해 보자

### 목차
[1. Travis CI 배포 자동화](#1-travis-ci-배포-자동화)<br>
[1.1 CI & CD 소개](#11-ci-&-cd-소개)<br>
[1.2 Travis CI 연동하기](#12-travis-ci-연동하기)<br>
[1.3 Travis CI와 AWS S3 연동하기](#13-travis-ci와-aws-s3-연동하기)<br>
[1.3 Travis CI와 AWS S3 연동하기](#13-travis-ci와-aws-s3-연동하기)<br>
[1.3 Travis CI와 AWS S3 연동하기](#13-travis-ci와-aws-s3-연동하기)<br>

## 1. Travis CI 배포 자동화
여러 개발자의 코드가 실시간으로 병합되고, 테스트가 수행되는 환경, master 브랜치가 푸시되면 배포가 자동으로 이루어지는 환경을 구축하지 않으면 실수할 여지가 너무나 많다. 지속 가능한 통합 환경을 구축하고 배포해야 한다.

### 1.1 CI & CD 소개
CI(Continuous Integration - 지속적 통합) : VCS 시스템에 PUSH가 되면 자동으로 테스트와 빌드가 수행되어 안정적인 배포 파일을 만드는 과정

CD(Continuous Deployment - 지속적인 배포) : 빌드 결과를 자동으로 운영 서버에 무중단 배포까지 진행되는 과정

일반적으로 CI만 구축되어 있지는 않고, CD도 함께 구축된 경우가 대부분이다.

하나의 프로젝트를 여러 개발자가 개발하게되는데 예전에는 각자가 개발한 코드를 매주 병합일을 정해서 각자 개발한 코드를 합치기만 했다. 이런 수작업은 생산성이 좋지 않기 때문에 개발자들은 지속 가능한 통합 환경(CI)를 구축했다.

여기서 주의할 점은 단순히 CI 도구를 도입했다고 해서 CI를 하고 있는 것은 아니다. CI에 대하 4가지 규칙이 있다.
- 모든 소스 코드가 살이 있고(현재 실행되고) 누구든 현재의 소스에 접근할 수 있는 단일 지점을 유지할 것
- 빌드 프로세스를 자동화해서 누구든 소스로부터 시스템을 빌드하는 단일 명령어를 사용할 수 있게 할 것
- 테스팅을 자동화해서 단일 명령어로 언제든지 시스템에 대한 건전한 테스트 수트를 실행할 수 있게 할 것
- 누구나 현재 실행 파일을 얻으면 지금까지 가장 완전한 실행 파일을 얻었다는 확신을 하게 할 것

여기서 특히나 중요한 것은 테스팅 자동화다. 지속적으로 통합하기 위해서는 무엇보다 이 프로젝트가 완전한 상태임을 보장하기 위해 테스트 코드가 구현되어 있어야만 한다.

### 1.2 Travis CI 연동하기
Travis CI는 깃헙에서 제공하는 무료 CI 서비스다. 젠킨스는 설치형이기 떄문에 이를 위한 EC2 인스턴스 하나가 더 필요하다. AWS에서 CI 도구로 CodeBuild를 제공하는데 빌드 시간만큼 요금이 발생한다.

- Travis CI 웹 서비스 설정
    - Travis 사이트에서 깃헙로그인
    - 계정명 > setting
    - 저장소를 찾고, 오른쪽 상태바를 활성화
    - 활성화한 저장소를 클릭하면 저장소 빌드 히스토리 페이지로 이동
- 프로젝트 설정
    - Travis CI의 상세한 설정은 프로젝트의 .travis.yml 파일로 할 수 있다.
        - YAML(야믈)은 쉽게 말해 JSON에서 괄호를 제거한 것이다. 기계에서 파싱하기 쉽게, 사람이 다루기 쉽게.
    - 프로젝트의 build.gradle과 같은 위치에 .travis.yml을 생성한다.
        ```properties
        language: java
        jdk:
        - openjdk8

        branches:
        only:
            - master

        # Travis CI 서버의 Home
        cache:
        directories:
            - '$HOME/.m2/repository'
            - '$HOME/.gradle'

        script: "./gradlew clean build"

        # CI 실행 완료 시 메일로 알람
        notifications:
        email:
            recipients:
            - 본인 메일 주소
        ```
        - branches
            - Travis CI를 어느 브랜치가 푸시될 때 수행할지 지정
            - 현재 옵션은 오직 master 브랜치에 push될 때만 수행한다.
        - cache
            - 그레이들을 통해 의존성을 받게 되면 이를 해당 디렉토리에 캐시하여, 같은 의존성은 다음 배포 때부터 다시 받지 않도록 설정한다.
        - notifications
            - Travis CI 실행 완료 시 자동으로 알람이 가다록 설정한다.

### 1.3 Travis CI와 AWS S3 연동하기