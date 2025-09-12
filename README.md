# smore-back

`s﻿more-back`은 학습 및 스터디 활동을 관리하는 백엔드 서비스입니다. 이 서비스는 스터디룸, 참여자, 집중도 기록, 포인트, 출석 등의 기능을 다룹니다.

<br>

<img width="1213" height="769" alt="image" src="https://github.com/user-attachments/assets/7a615091-4161-4a48-9bfe-634288a823dd" />

---

##  기능 목록
- **스터디룸 관리**  
  - 스터디룸 생성, 조회, 수정, 삭제
  - 참여자 초대 및 관리
- **참여자(유저) 관리**  
  - 회원가입 및 로그인  
  - 프로필 관리
- **집중도(포커스) 기록 기능**  
  - 사용자의 집중 시간 기록 및 조회  
  - 일/주/월별 집중도 통계 제공
- **포인트 시스템**  
  - 학습 활동에 따른 포인트 적립 및 차감 기능  
  - 활동 보상 및 리워드 시스템 연동 가능
- **출석 관리 기능**  
  - 스터디룸별 출석 기록 기능 (예: 출석 체크, 지각 등)  
  - 출석 현황 통계 및 리포트 기능 제공
---
## 📦 Dependencies

| 항목 | 버전/설명 |
|------|-----------|
| **Java** | 17 이상 |
| **Spring Boot** | 3.x (Gradle 기반) |
| **Spring Web** | REST API 개발 |
| **Spring Security** | 인증/인가 처리 |
| **Spring Data JPA** | ORM, 데이터베이스 액세스 |
| **OAuth2 Client** | 소셜 로그인(Kakao 등) |
| **MySQL Driver** | MySQL 연결용 JDBC 드라이버 |
| **Lombok** | 보일러플레이트 코드 감소 |
| **Validation (Jakarta Validation)** | 요청 파라미터 유효성 검사 |
| **Jackson** | JSON 직렬화/역직렬화 |
| **Springdoc OpenAPI** | API 문서화(Swagger UI) |
| **JUnit 5** | 단위/통합 테스트 |
| **Mockito** | 테스트용 Mock 객체 생성 |
| **Redis Client (spring-data-redis)** | 캐싱, 토큰 저장 |
| **Dockerfile** | 컨테이너 빌드/배포 지원 |

---

<br>

##  Getting Started

### 1. Clone the repository  
```bash
git clone https://github.com/5-re-5/smore-back.git
cd smore-back
```
### 2. Install dependencies
```bash
npm install
# 또는
yarn install
```
### 3. Environment setup
프로젝트 루트에 .env 파일 생성 후 다음 항목 설정:

```env
DATABASE_URL=postgresql://username:password@localhost:5432/smoredb
JWT_SECRET=your_jwt_secret_key
PORT=3000
```

### 4. Run database migrations (ORM에 따라 명령 다름)
- Prisma:

```bash
npx prisma migrate dev --name init
```
- TypeORM:

```bash
npx typeorm migration:run
```

### 5. Start the server
```bash
npm run dev
# 또는
yarn dev
```

http://localhost:8081 에서 서버가 실행됩니다.

### 6. API 테스트
Postman, Insomnia 또는 Swagger 등을 이용해 엔드포인트 테스트를 진행할 수 있습니다.

<br>

## API Endpoints

- **POST** `/api/auth/signup` — 회원가입  
- **POST** `/api/auth/login` — 로그인 (JWT 발급)  
- **GET** `/api/users/me` — 사용자 정보 조회 (인증 필요)  
- **GET** `/api/rooms` — 스터디룸 목록 조회  
- **POST** `/api/rooms` — 스터디룸 생성  
- **GET** `/api/rooms/:roomId` — 특정 스터디룸 정보 조회  
- **PUT** `/api/rooms/:roomId` — 스터디룸 정보 수정  
- **DELETE** `/api/rooms/:roomId` — 스터디룸 삭제  
- **POST** `/api/rooms/:roomId/join` — 스터디룸 참가 요청  
- **GET** `/api/rooms/:roomId/participants` — 참여자 목록 조회  
- **POST** `/api/focus-records` — 집중도 기록 생성  
- **GET** `/api/focus-records?userId=&roomId=&start=&end=` — 집중도 기록 조회 및 필터링  
- **GET** `/api/user/:userId/points` — 사용자 포인트 조회  
- **POST** `/api/user/:userId/points` — 포인트 조정 (적립/차감)  
- **POST** `/api/attendance` — 출석 체크  
- **GET** `/api/attendance?roomId=&date=` — 출석 현황 조회  

---

<br>

## Folder Structure

```plaintext
└── smore-back/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   │   └── org/
    │   │   │       └── oreo/
    │   │   │           └── smore/
    │   │   │               ├── domain/           # 도메인별 패키지 (auth, user, studyroom, focusrecord 등)
    │   │   │               │   ├── auth/         # JWT, OAuth2, Security 설정
    │   │   │               │   ├── user/         # 사용자 엔티티, 서비스, 컨트롤러
    │   │   │               │   ├── studyroom/    # 스터디룸 관련 로직
    │   │   │               │   ├── focusrecord/  # 집중도 기록
    │   │   │               │   └── common/       # 공통 유틸, 예외 처리
    │   │   │               └── global/           # 전역 설정, 시큐리티, 환경설정
    │   │   └── resources/
    │   │       ├── application.properties        # 기본 설정
    │   └── test/
    │       └── java/
    │           └── org/
    │               └── oreo/
    │                   └── smore/                # 테스트 코드
    ├── build.gradle
    ├── settings.gradle
    ├── Dockerfile
    ├── README.md
    └── .env
```


## Testing

본 프로젝트는 단위/슬라이스/통합 레벨에서 테스트를 작성하여 안정성을 확보했습니다.
컨트롤러의 예외 매핑, 서비스의 비즈니스 규칙, 저장소 쿼리, 외부 연동(Webhook/Flask)까지 커버합니다.

### 테스트 도구 및 환경

- JUnit 5, Mockito

- Spring Boot Test: @WebMvcTest, @DataJpaTest, @SpringBootTest

- Testcontainers: MySQL, Redis (로컬에 Docker 필요)

- H2 인메모리 DB: 빠른 슬라이스 테스트용

- ObjectMapper, MockMvc, TestEntityManager


### 커버리지 범위

| 레이어      | 주요 검증 항목                        | 대표 시나리오                                       |
|-------------|---------------------------------------|----------------------------------------------------|
| Controller  | 요청/응답 포맷, 인증 필터, 전역 예외 매핑 | 비참여자 접근 시 403, 최대 인원 초과 시 409, 존재하지 않는 리소스 404 |
| Service     | 비즈니스 규칙, 트랜잭션 경계, 캐시 전략  | 스터디룸 입장/퇴장, 중복 출석 차단, 집중도 기록 검증         |
| Repository  | 쿼리 정확성, 페이징/정렬, 인덱스 활용     | 기간별 집중도 집계, 룸별/유저별 조회                         |
| External    | LiveKit Webhook, Flask(API) 통신      | 참여자 이벤트 수신 및 카운팅, 모델 API 실패 시 복구 로직         |



### 실행 방법
```
# 전체 테스트
./gradlew test

# 특정 패키지/클래스만
./gradlew test --tests "*StudyRoom*"
./gradlew test --tests "org.oreo.smore.api.StudyRoomControllerTest"

# CI 환경에서 (JUnit XML + 커버리지 리포트 생성)
./gradlew clean test jacocoTestReport
```

Testcontainers(통합 테스트)는 Docker가 필요합니다. Docker가 없으면 슬라이스 테스트만 우선 실행하세요.

### 외부 연동 모킹 전략

- LiveKit Webhook: Controller 단에서 서명 검증을 우회(테스트용 빈/프로퍼티)하고 이벤트 JSON을 직접 주입.

- Flask(집중도/AI) API: `RestTemplateBuilder`/`WebClient`를 주입받도록 설계하고, 테스트에서는 `MockRestServiceServer` 또는 `Mockito`로 스텁.

- 장애 시나리오: 타임아웃/5xx 응답을 스텁해 재시도/폴백 동작 검증.

테스트 데이터 관리

- Fixture Builder 패턴(정적 팩토리)로 엔티티 생성: `UserFixture`, `StudyRoomFixture`, `FocusRecordFixture`

- 슬라이스 테스트: H2 사용, `@DataJpaTest` + `TestEntityManager`

- 통합 테스트: Testcontainers(MySQL/Redis)로 실제와 유사한 환경
