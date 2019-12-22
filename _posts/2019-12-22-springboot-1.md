---
title: "스프링부트 - 1"
date: 2019-12-22 10:03:00 -0400
categories: spring
---

스프링부트 - 1

### 목차
[1. 스프링 부트 시작해보기](#1-스프링-부트-시작해보기)<br>
[2. 스프링 부트 원리](#2-스프링-부트-원리)<br>
[3. 스프링 부트 활용](#3-스프링-부트-활용)<br>

## 1. 스프링 부트 시작해보기
Intellij Ultimate로 생성하거나 [Initializr](https://start.spring.io/)사이트에서 프로젝트생성하고 다운로드 받는다.

### 1.1 jar패키징, 실행
1. 터미널에서 'mvn package' 입력한다.
2. jar 파일을 실행한다.  'java -jar /target/demospringboot-0.0.1-SNAPSHOT.jar
3. http://localhost:8080/ 으로 들어가 whitelabel page 확인
4. Ctrl + C 로 jar 실행 중지

### 1.2 스프링 부트 프로젝트 구조
메이븐 기본 프로젝트 구조와 동일
 - 소스 코드 (src\main\java)
 - 소스 리소스 (src\main\resource)
 - 테스트 코드 (src\test\java)
 - 테스트 리소스 (src\test\resource)

메인 애플리케이션 위치 (psvm이 있는 class)
 - 기본 패키지 (component scan을 여기서부터 하기 때문)

 ## 2. 스프링 부트 원리

 ### 2.1 의존성 관리 이해
 [document](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-dependency-management) <br>

 pom.xml > spring-boot-starter-parent > spring-boot-dependencies <br>
 하나씩 타고 올라가 보면 의존성들이 다 정의되어 있다.

우리가 직접 관리해야 할 의존성들이 줄어 들어 관리하기 편하다.

### 2.1 의존성 관리 응용
- 버전 관리 해주는 의존성 추가
- 버전 관리 안해주는 의존성 추가
  - 버전을 명시하는 게 best practice
- 기존 의존성 버전 변경하기
  - spring-boot-starter-parent
  - Spring Boot Dependencies
- https://mvnrepository.com/


### 2.2 자동 설정 이해
```java
@SpringBootApplication
public class DemospringbootApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemospringbootApplication.class, args);

    // 위의 코드와 같다.
		SpringApplication application = new SpringApplication(DemospringbootApplication.class);
    // 웹으로 실행하고 싶지 않은 경우
    //application.setWebApplicationType(WebApplicationType.NONE);
		application.run(args);
	}

}
```

- @EnableAutoConfiguration (@SpringBootApplication 안에 숨어 있음)
- 빈은 사실 두 단계로 나눠서 읽힘
  - 1단계: @ComponentScan
  - 2단계: @EnableAutoConfiguration
- @ComponentScan
  - 애노테이션이 있는 클래스와 이하의 패키지들을 스캔하여 빈으로 등록
  - @Component
  - @Configuration @Repository @Service @Controller @RestController
- @EnableAutoConfiguration
  - spring.factories
    - org.springframework.boot.autoconfigure.EnableAutoConfiguration
  - @Configuration
  - @ConditionalOnXxxYyyZzz

### 2.3 스프링 부트 원리 정리
스프링 부트 원리 정리
- 의존성 관리
  - 이것만 넣어도 이만큼이나 다 알아서 가져오네?
- 자동 설정
  - @EnableAutoConfiguration이 뭘 해주는지 알겠어.
- 내장 웹 서버
  - 아 스프링 부트가 서버가 아니라 내장 서버를 실행하는 거군.
- 독립적으로 실행 가능한 JAR
  - spring-boot-maven 플러그인이 이런걸 해주는구나..


## 3. 스프링 부트 활용

### 3.1 SpringApplication - 1
https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-spring-application.html#boot-features-spring-application

```java
SpringApplication.run()... 
// 스프링 애플리케이션이 제공하는 커스텀 기능을 사용하기 어려우므로 
```
```java
@SpringBootApplication
public class DemospringbootApplication {
	public static void main(String[] args) {
		SpringApplication app = new SpringApplication(DemospringbootApplication.class);
		app.run(args);
	}
}
```
- 인스턴스를 만들어서 run하는 방법으로 사용하자.

- 아무 것도 하지않으면 애플리케이션의 기본 로그 레벨이 INFO이다.

- 'VM options : -Ddebug'  설정시 디버그모드로 애플리케이션이 실행되며, 어떤 자동설정이 적용되고 적용되지 않았는지 확인 가능, 로그가 DEBUG 레벨까지 확인이 가능하다.

- FailureAnalyzer : 에러 발생 시, 에러 메시지를 예쁘게 출력해준다. 

- 배너
  - banner.txt | gif | jpg | png
  - 애플리케이션 실행시 에디터에서 보여지는 이미지 등.. 변경하고 싶으면 src/resources에 banner.txt 파일을 생성하고 배너텍스트를 입력하면 애플리케이션 실행시 커스텀배너가 사용된다. 원한다면 아스키 제너레이터를 사용해서 예쁘게 꾸밀 수 있다.
  - ${spring-boot.version} 등의 변수를 사용할 수 있다.
  - 배너 위치는 resources에 넣거나 다른 곳에 위치시키면 application.properties에 경로를 지정한다. spring.banner.location=../.../
  - 배너 끄기 : SpringApplciation app.setBannerMode(Mode.Off);

- SpringApplicationBuilder로 빌터 패턴 사용 가능
```java
public static void main(String[] args) {
		new SpringApplicationBuilder()
        .main(SpringApplication.class)
        .banner(...)
        .run(args);
}
```


### 3.2 SpringApplication - 2 
