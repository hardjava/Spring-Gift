# Spring Gift

카카오톡 선물하기를 기반으로 상품 관리, 회원 인증, 위시리스트, 상품 옵션, 주문 기능을 단계적으로 개발한 백엔드 프로젝트입니다.

요구사항이 확장될 때마다 저장 방식과 도메인 구조를 개선했으며, `Java Collection → JdbcTemplate → Spring Data JPA` 순서로 데이터 접근 기술을 발전시켰습니다. 이후 카카오 API 연동, 테스트 코드 작성, AWS EC2 배포를 진행했습니다.

---

## 프로젝트 정보

| 구분    | 내용                   |
| ----- | -------------------- |
| 개발 기간 | 2025.06 ~ 2025.08    |
| 개발 인원 | 1명                   |
| 담당 역할 | 백엔드 개발               |
| 개발 방식 | 4개의 미션을 통한 단계별 기능 확장 |

## 기술 스택

`Java 21` `Spring Boot` `Spring Data JPA` `JdbcTemplate` `H2`
`Thymeleaf` `JWT` `BCrypt` `JUnit 5` `GitHub Actions` `AWS EC2`

---

## 프로젝트 구성

| Mission   | Repository                                                                     | 주요 내용                            |
| --------- | ------------------------------------------------------------------------------ | -------------------------------- |
| Mission 1 | [spring-gift-product](https://github.com/hardjava/spring-gift-product)         | 상품 CRUD, 관리자 화면, H2·JdbcTemplate |
| Mission 2 | [spring-gift-wishlist](https://github.com/hardjava/spring-gift-wishlist)       | 유효성 검사, JWT 인증, 위시리스트            |
| Mission 3 | [spring-gift-enhancement](https://github.com/hardjava/spring-gift-enhancement) | JPA 전환, 페이지네이션, 상품 옵션            |
| Mission 4 | [spring-gift-order](https://github.com/hardjava/spring-gift-order)             | 카카오 로그인, 주문, 자동 배포               |

---

<details>
<summary><b>Mission 1. 상품 관리</b></summary>

<br>

[spring-gift-product 바로가기](https://github.com/hardjava/spring-gift-product)

### 1단계 - 상품 API

* Product 도메인과 요청·응답 DTO 구성
* 상품 목록 및 상세 조회 API 개발
* 상품 등록, 전체 수정, 일부 수정, 삭제 API 개발
* Java Collection 기반 상품 저장소 구성
* 존재하지 않는 상품에 대한 예외 처리
* 요청값 검증과 공통 예외 응답 적용

### 2단계 - 관리자 화면

* Thymeleaf 기반 상품 관리 화면 개발
* 상품 목록 및 상세 페이지 개발
* 상품 등록·수정·삭제 기능 개발
* `HiddenHttpMethodFilter`를 이용한 PUT·DELETE 요청 처리
* 입력값 검증과 오류 메시지 표시

### 3단계 - 데이터베이스 적용

* H2 데이터베이스 설정
* `schema.sql`, `data.sql` 작성
* Repository 인터페이스를 통한 저장소 추상화
* JdbcTemplate 기반 ProductRepository 개발
* RowMapper를 이용한 조회 결과 매핑
* 에러 응답 전용 DTO 적용
* 상품 API 테스트 코드 보완

</details>

---

<details>
<summary><b>Mission 2. 회원 인증 및 위시리스트</b></summary>

<br>

[spring-gift-wishlist 바로가기](https://github.com/hardjava/spring-gift-wishlist)

### 1단계 - 유효성 검사 및 예외 처리

* 상품 등록·수정 요청에 유효성 검사 적용
* 상품명 길이와 허용 특수문자 검증
* 상품 가격 검증
* 상품명에 `카카오`가 포함된 경우 승인 여부 검증
* 커스텀 검증 어노테이션과 Validator 구성
* 검증 실패 항목별 오류 메시지 반환
* 잘못된 요청에 대한 400 응답 테스트

### 2단계 - 회원가입 및 로그인

* Member 도메인과 Role 구성
* JdbcTemplate 기반 MemberRepository 개발
* 회원가입 및 로그인 API 개발
* 이메일 중복 검증
* BCrypt 기반 비밀번호 암호화
* 로그인 성공 시 JWT 발급
* JWT 만료 시간과 사용자 권한 적용
* 인증·인가 실패 상황별 예외 처리
* 회원가입·로그인·권한 검증 테스트

### 3단계 - 위시리스트

* Wish와 WishSummary 도메인 구성
* JdbcTemplate 기반 WishListRepository 개발
* 위시리스트 조회·등록·삭제 API 개발
* 상품별 위시리스트 등록 수 집계
* `@LoginMember` 커스텀 어노테이션 작성
* `HandlerMethodArgumentResolver`를 이용한 회원 정보 주입
* 위시리스트 Controller·Service 테스트 작성

</details>

---

<details>
<summary><b>Mission 3. 상품 고도화</b></summary>

<br>

[spring-gift-enhancement 바로가기](https://github.com/hardjava/spring-gift-enhancement)

### 1단계 - JPA 엔티티 매핑

* Member, Product, Wish 엔티티 매핑
* 회원·상품·위시리스트 연관관계 설정
* 공통 생성·수정 시간을 위한 BaseEntity 구성
* JdbcTemplate 기반 저장소를 Spring Data JPA로 전환
* JPA 변경 감지를 활용한 데이터 수정
* `@DataJpaTest` 기반 Repository 테스트
* 상품명과 가격 검증을 값 객체로 분리

### 2단계 - 페이지네이션

* Pageable 기반 상품 목록 페이지네이션
* Pageable 기반 위시리스트 페이지네이션
* 페이지 번호·크기·정렬 조건 처리
* 페이지 정보 응답 DTO 구성
* Thymeleaf 페이지 이동 기능 적용
* 상품 및 위시리스트 페이지 조회 테스트

### 3단계 - 상품 옵션

* Option 엔티티 구성
* Product와 Option의 일대다 연관관계 설정
* 상품 등록 시 하나 이상의 옵션 포함
* 옵션명 길이와 허용 문자 검증
* 동일 상품 내 옵션명 중복 방지
* 옵션 수량과 재고 차감 규칙 적용
* 재고 부족 및 잘못된 수량 예외 처리
* 상품 옵션 목록 조회 API 개발
* OptionRepository, OptionService, OptionController 구성
* 도메인·서비스·통합 테스트 작성

</details>

---

<details>
<summary><b>Mission 4. 주문 및 배포</b></summary>

<br>

[spring-gift-order 바로가기](https://github.com/hardjava/spring-gift-order)

### 1단계 - 카카오 로그인

* 카카오 로그인 URL 생성
* 인가 코드 Callback Controller 구성
* 인가 코드를 이용한 액세스 토큰 요청
* RestClient 기반 카카오 API 통신
* 카카오 ID 토큰 검증
* 카카오 사용자 정보 조회
* 기존 회원 조회 또는 신규 회원 가입 처리
* OAuth 제공자와 액세스 토큰 정보 관리
* 외부 API 오류 응답 처리
* 카카오 로그인 테스트 작성

### 2단계 - 주문

* Order 엔티티와 Repository 구성
* OrderService와 OrderController 구성
* 주문 요청·응답 DTO 작성
* 상품 옵션과 주문 수량을 이용한 주문 생성
* 주문 수량만큼 옵션 재고 차감
* 주문 메시지 저장
* 주문 상품을 위시리스트에서 자동 삭제
* 카카오 로그인 회원에게 주문 내역 메시지 전송
* 재고 차감·위시리스트 삭제·주문 저장을 하나의 트랜잭션으로 처리
* 주문 도메인·서비스·Controller 테스트 작성

### 3단계 - 배포

* AWS EC2 애플리케이션 배포
* GitHub Actions Workflow 작성
* 특정 브랜치 Push 시 자동 배포
* GitHub Secrets를 이용한 설정값 관리
* EC2 SSH 접속 후 Gradle 빌드
* 기존 프로세스 종료 후 신규 JAR 실행
* 애플리케이션 로그 파일 관리
* CORS 설정과 MockMvc 기반 검증

</details>

---

## 단계별 기술 확장

```text
Java Collection
       ↓
H2 + JdbcTemplate
       ↓
Spring Data JPA
       ↓
카카오 API 연동
       ↓
GitHub Actions + AWS EC2
```

