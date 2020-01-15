---
title: "interview"
date: 2000-01-01 10:03:00 -0400
categories: interview
---

개발자 면접 예상 질문 정리


- GET, POST
    - GET 가져오는 것이고 POST는 수행하는 것이다.
    - GET 서버로부터 정보를 조회하기 위해 설계된 메소드이다.
    - GET 요청을 전송할 때 필요한 데이터를 Body에 담지 않고, 쿼리스트링을 통해 전송한다.
        - ex) www.example-url.com/resources?name1=value1&name2=value2
    - GET은 불필요한 요청을 제한하기 위해 요청이 캐시될 수 있습니다
    - POST는 리소스를 생성/변경하기 위해 설계되었기 때문에 GET과 달리 전송해야될 데이터를 HTTP 메세지의 Body에 담아서 전송한다.
    - HTTP 메세지의 Body는 길이의 제한없이 데이터를 전송할 수 있다. POST 요청은 GET과 달리 대용량 데이터를 전송할 수 있다. 
    - 내용이 눈에 보이지 않아 GET보다 보안적인 면에서 안전하다고 생각할 수 있지만, POST 요청도 크롬 개발자 도구, Fiddler와 같은 툴로 요청 내용을 확인할 수 있기 때문에 민감한 데이터의 경우에는 반드시 암호화해 전송해야 합니다.
    - POST로 요청을 보낼 때는 요청 헤더의 Content-Type에 요청 데이터의 타입을 표시해야 합니다. 데이터 타입을 표시하지 않으면 서버는 내용이나 URL에 포함된 리소스의 확장자명 등으로 데이터 타입을 유추합니다. 만약, 알 수 없는 경우에는 application/octet-stream로 요청을 처리합니다.
    - GET은 Idempotent, POST는 Non-idempotent하게 설계되었습니다.
        - 수학에서연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질
        - 즉, 멱등이라는 것은 동일한 연산을 여러 번 수행하더라도 동일한 결과가 나타나야 합니다.
    -  GET으로 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 한다는 것을 의미합니다. 이에 따라 GET은 설계원칙에 따라 서버의 데이터나 상태를 변경시키지 않아야 Idempotent하기 때문에 주로 조회를 할 때에 사용해야합니다.
    - POST는 Non-idempotent하기 때문에 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있습니다. 이에 따라 POST는 서버의 상태나 데이터를 변경시킬 때 사용됩니다. 게시글을 쓰면 서버에 게시글이 저장이 되고, 게시글을 삭제하면 해당 데이터가 없어지는 등 POST로 요청을 하게 되면 서버의 무언가는 변경되도록 사용됩니다. 이처럼 POST는 생성, 수정, 삭제에 사용할 수 있지만, 생성에는 POST, 수정은 PUT 또는 PATCH, 삭제는 DELETE가 더 용도에 맞는 메소드라고 할 수 있습니다.
    - 마지막으로 웹페이지를 조회할 때, 링크를 통해 특정 페이지로 바로 이동하려면 해당 링크와 관련된 정보가 필요한데 POST는 요청 데이터가 Body에 담겨 있기 때문에 링크 정보를 가져올 수 없습니다. 반면, GET은 URL에 요청 파라미터를 가지고 있기 때문에 링크를 걸 때, URL에 파라미터를 사용해 더 디테일하게 페이지를 링크할 수 있습니다.

- AOP
    - Aspect Orientied Programming
    - 흩어진 코드를 모아서 코딩하자.
    - 핵심기능과 공통기능을 분리해서 공통기능을 필요로 하는 핵심 기능들에 사용하는 방식
    - 스프링에서는 프록시를 이용해 AOP를 구현한다.

- 추상클래스, 인터페이스
    - 추상클래스는 만들어야 할 여러 클래스들의 공통점을 찾아 추상화시켜서 사용하는 것이 개발에서 이득일 때 사용한다.
    - 추상클래스는 추상메서드가 없어도 된다.
    - 추상 클래스는 일반적으로 베이스 클래스로 상속해서 더 구체적인 클래스를 만들 때 쓰기 좋다.
    - 인터페이스는 함수의 껍데기만 있는데, 그 이유는 그 함수의 구현을 강제하기 위해서다.
    - 구현 객체가 같은 동작을 한다는 것을 보장하기 위한 목적이다.
    - 클래스가 아니므로 다중 상속이 가능하다.

- mysql innodb

- DI(Defendency Injection)
    - 객체 자체가 아니라 Framework에 의해 객체의 의존성 주입입되는 설계 패턴
    - 의존성 주입법 : constructor, setter, field

- JPA, Hibernate, Spring Data JPA
    - JPA(Java Persistance Interfae) 애플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스이다. JPA는 특정 기능을 하는 라이브러리가 아니다. 단순명세이므로 구현이 없다.
    - Hibernate는 JPA의 구현체이다. JPA의 인터페이스를 구현한 라이브러리이다. JPA를 사용하기 위해서 반드시 Hibernate를 사용할 필요가 없다.
    - Spring Data JPAsms Spring에서 제공하는 모듈 중 하나로 개발자가 JPA를 더 쉽게 사용할 수 있게 도와준다. JPA를 한 단계 더 추상화시킨 Repository라는 인터페이스를 제공함으로써 이루어진다.
    - EntityManager를 직접 사용한다면 JPA를 사용하는 것이고, EntityManager가 아닌 Repository를 구현해서 사용한다면 Spring Data JPA를 사용하는 것이다.

- REST API
    - API
        -Application Programming Interface
    - REST
        - REpresentational State Transfer
        - 인터넷 상의 시스템 간의 상호 운용성(interoperability)을 제공하는 방법중 하나
        - 시스템 제각각의 독립적인 진화를 보장하기 위한 방법
        - REST API: REST 아키텍처 스타일을 따르는 API

- if, switch 차이
    - if
        - branch statement에 기반을 두고 있다.
        - 점프 테이블을 만드는 오버헤드 없다.
        - if 혹은 else if를 만날 때마다 만족하는지 아닌지를 확인하기 위한 인스트럭션이 계속 필요함
        - 따져야 할 조건의 수가 적을 때는 if~else가 유리함
    - switch
        - jump statement에 기반을 두고 있다.
        - 입력값으로 받은 변수 값만큼 점프 테이블을 만들어야 한다.
        - 시작시에 입력받은 값을 확인하는 인스트럭션만 필요, 조건을 확인하는 인스트럭션 필요 없음
        - 점프테이블을 만드는 오버헤드 있음
        - 따져야할 조건이 많은 경우 유리하다.

- 자바 람다식
    - 메서드를 하나의 식으로 표현한 것
    - 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로 익명함수라고도 한다.
    - 람다식은 메서드의 매개변수로 전달될 수 있고 메서드의 결과로 반환될 수 있다. 즉 메서드를 변수처럼 다루는 것이 가능하다.
    ```java
    int max(int a, int b) {
        return a > b? a : b;
    }

    (int a, int b) -> {
        return a > b? a : b;
    }

    (int a, int b) -> a > b? a : b

    (a, b) -> a > b? a : b

    a -> a * a
    ```

    - 함수형 인터페이스
        - 람다식을 다루기 위한 인터페이스
        - 람다식은 메서드와 동등한 것이 아니라 익명클래스의 객체와 동등하다.
    ```java
    // 람다식
    (int a, int b) -> a > b? a : b

    // 익명 클래스의 객체
    new Object() {
        int max(int a, int b) {
            return a > b? a : b;
        }
    }
    ```

    - 메서드 참조(Method reference)
        - 람다식이 하나의 메서드만 호출하는 경우, 메소드 참조를 통해 람다식을 간략히 할 수 있다.
    ```java
    Function<String, Integer> f = (String s) -> Integer.parseInt(s);
    Function<String, Integer> f = Integer::parseInt;

    Supplier<MyClass> s = () -> new MyClass();
    Supplier<MyClass> s = MyClass::new;

    Function<Integer, int[]> f = x -> new int[x];
    Function<Integer, int[]> f2 = int[]::new;
    ```
- 자바 옵셔널

- 자바 스트림

- 클로저

- 자바 배열의 숫자를 내림,오름차순으로 정렬하는 소스코드

- SQL, NoSQL

- main.js에서 var main = {...} 라는 코드를 선언하고 변수의 속성으로 function을 추가한 이유는?
    - 나중에 다른 js가 추가 되어 같은 이름의 함수가 생기게 되면 먼저 브라우저에서 먼저 로딩된 함수가 덮어쓰게 된다.
    - 여러 사람이 참여하는 프로젝트에서는 중복된 함수 이름은 자주 발생할 수 있다. 이런 문제를 피하려고 main.js만의 유효범위를 만들어 사용한다.
    - var main이란 객체를 만들어 해당 객체에서 필요한 모든 function을 선언한다. index 객체 안에서만 function이 유효하기 때문에 다른 js와 겹칠 위험이 사라진다.