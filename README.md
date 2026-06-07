# Spring Gift

카카오톡 선물하기를 기반으로 상품 관리부터 회원 인증, 위시리스트, 상품 옵션, 주문까지 단계적으로 개발한 백엔드 프로젝트입니다.

기능 요구사항이 확장되는 과정에 맞춰 저장 구조와 도메인 모델을 개선하고, 인증·인가, 외부 API 연동, 테스트 코드를 적용했습니다.

## Tech Stack

* Java 21
* Spring Boot
* Spring Data JPA
* H2
* Thymeleaf
* JWT
* JUnit 5

## Project Stages

| 단계                | 저장소                                                                            | 주요 내용                                               |
| ----------------- | ------------------------------------------------------------------------------ | --------------------------------------------------- |
| 1. 상품 관리          | [spring-gift-product](https://github.com/hardjava/spring-gift-product)         | 상품 CRUD REST API, Thymeleaf 관리자 페이지, 입력값 검증 및 예외 처리 |
| 2. 인증 및 위시리스트     | [spring-gift-wishlist](https://github.com/hardjava/spring-gift-wishlist)       | BCrypt 비밀번호 암호화, JWT 인증·인가, 위시리스트 기능                |
| 3. 기능 고도화         | [spring-gift-enhancement](https://github.com/hardjava/spring-gift-enhancement) | JPA 엔티티 모델링, 연관관계 매핑, 페이지네이션, 상품 옵션 및 재고 관리         |
| 4. 주문 및 외부 API 연동 | [spring-gift-order](https://github.com/hardjava/spring-gift-order)             | 주문 처리, 옵션 수량 차감, 카카오 로그인 API 및 카카오톡 메시지 연동          |

## 주요 개발 내용

### 1. 상품 관리

* 상품 등록, 조회, 수정, 삭제 REST API 개발
* Thymeleaf 기반 상품 관리자 페이지 개발
* 상품명, 가격, 이미지 URL 입력값 검증
* 공통 예외 응답 구조 작성

### 2. 회원 인증 및 위시리스트

* BCrypt 기반 비밀번호 암호화
* JWT 발급 및 인증·인가 처리
* 로그인 회원의 위시리스트 등록과 삭제 기능 개발
* 커스텀 어노테이션과 ArgumentResolver를 활용한 회원 정보 주입

### 3. 도메인 및 상품 옵션 고도화

* 회원, 상품, 위시리스트, 옵션 엔티티 모델링
* JPA 기반 연관관계 매핑
* 상품 목록 페이지네이션 적용
* 옵션 이름 중복, 허용 문자, 수량 등의 비즈니스 규칙 검증

### 4. 주문 및 카카오 API 연동

* 상품 옵션과 수량을 기반으로 주문 처리
* 주문 완료 후 옵션 재고 차감
* 주문 상품의 위시리스트 자동 삭제
* 카카오 로그인 API를 통한 사용자 인증
* 주문 결과 카카오톡 메시지 전송

## 테스트

* MockMvc 기반 Controller 테스트
* DataJpaTest 기반 Repository 테스트
* SpringBootTest 기반 통합 테스트
* 인증·인가, 상품 조회, 페이지네이션, 주문 정상 및 예외 상황 검증

## Repository

* [spring-gift-product](https://github.com/hardjava/spring-gift-product)
* [spring-gift-wishlist](https://github.com/hardjava/spring-gift-wishlist)
* [spring-gift-enhancement](https://github.com/hardjava/spring-gift-enhancement)
* [spring-gift-order](https://github.com/hardjava/spring-gift-order)
