# 🌱 Plant Community Platform

> 식물 애호가들을 위한 종합 커뮤니티 플랫폼

![Java](https://img.shields.io/badge/Java-17-007396?style=flat-square&logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.9-6DB33F?style=flat-square&logo=spring-boot)
![MyBatis](https://img.shields.io/badge/MyBatis-3.0.5-000000?style=flat-square)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb)
![WebSocket](https://img.shields.io/badge/WebSocket-STOMP-010101?style=flat-square)

## 📋 프로젝트 소개

식물을 사랑하는 사람들이 모여 정보를 공유하고, 일정을 관리하며, 실시간으로 소통할 수 있는 종합 커뮤니티 플랫폼입니다.

### 주요 기능

#### 🌿 핵심 기능
- **식물 도감 및 관리**: 다양한 식물 정보 제공 및 개인 식물 관리
- **커뮤니티 게시판**: 게시글 작성, 댓글, 좋아요 기능
- **실시간 채팅**: WebSocket 기반 실시간 1:1 및 그룹 채팅
- **팔로우 시스템**: 관심있는 사용자 팔로우 및 피드 확인

#### 📅 일정 관리
- **식물 관리 캘린더**: 물주기, 영양제, 분갈이 일정 관리
- **한국 공휴일 연동**: 자동 공휴일 표시 및 일정 조정

#### ☀️ 날씨 연동
- **Kakao API 연동**: 실시간 날씨 정보 제공
- **식물 관리 알림**: 날씨에 따른 식물 관리 팁 제공

#### 🔔 메시지 시스템
- **알림 기능**: 댓글, 좋아요, 팔로우 알림
- **쪽지 기능**: 사용자 간 개인 메시지

## 🛠 기술 스택

### Backend
- **Framework**: Spring Boot 3.4.9
- **Language**: Java 17
- **ORM**: MyBatis 3.0.5
- **Database**: MariaDB
- **Real-time**: WebSocket (STOMP)

### Library & Tools
- **Lombok**: 보일러플레이트 코드 감소
- **JSoup**: HTML 파싱 및 이미지 추출
- **Log4jdbc**: SQL 쿼리 로깅
- **Date-holidays**: 한국 공휴일 처리

### API
- **Kakao API**: 날씨 정보 제공

## 📁 프로젝트 구조

```
src/main/java/com/green/backend_plant_comunity/
├── board/          # 게시판 기능
├── calendar/       # 캘린더 및 일정 관리
├── category/       # 카테고리 관리
├── chat/           # 실시간 채팅
├── comment/        # 댓글 시스템
├── environment/    # 환경 설정
├── follow/         # 팔로우 시스템
├── like/           # 좋아요 기능
├── member/         # 회원 관리
├── message/        # 메시지/알림
├── plant/          # 식물 정보 관리
├── weather/        # 날씨 정보
├── config/         # 설정 파일
│   ├── WebConfig.java
│   └── WebSocketConfig.java
└── util/           # 유틸리티
    ├── FileUploadUtil.java
    ├── HtmlImageParser.java
    └── ImageCleanupScheduler.java
```

## 🚀 주요 구현 사항

### 1. 실시간 채팅 시스템
```java
// WebSocket STOMP 프로토콜을 활용한 실시간 양방향 통신 구현
- 1:1 채팅 및 그룹 채팅 지원
- 메시지 읽음 처리
- 온라인 상태 표시
```

### 2. 이미지 관리 시스템
```java
// 게시글 작성 시 업로드된 이미지 자동 관리
- HTML 컨텐츠에서 이미지 추출 (JSoup)
- 미사용 이미지 자동 삭제 스케줄러
- 파일 업로드 유틸리티
```

### 3. 캘린더 일정 관리
```java
// 식물 관리를 위한 개인 일정 시스템
- 물주기, 영양제, 분갈이 일정 등록
- 반복 일정 설정
- 한국 공휴일 자동 표시
```

### 4. 소셜 기능
```java
// 사용자 간 상호작용 기능
- 팔로우/언팔로우
- 좋아요 및 북마크
- 댓글 시스템
```

## ⚙️ 설치 및 실행

### 필수 요구사항
- Java 17 이상
- MariaDB 10.x
- Gradle 8.x

### 설정 파일

`src/main/resources/application.properties`
```properties
# 데이터베이스 설정
spring.datasource.url=jdbc:mariadb://localhost:3306/your_database
spring.datasource.username=your_username
spring.datasource.password=your_password

# 파일 업로드 경로
file.upload-dir=/path/to/upload/directory

# Kakao API Key
kakao.api.key=your_kakao_api_key
```

### 실행 방법

```bash
# 1. 저장소 클론
git clone https://github.com/yourusername/plant-community.git

# 2. 프로젝트 디렉토리로 이동
cd plant-community

# 3. Gradle 빌드
./gradlew build

# 4. 애플리케이션 실행
./gradlew bootRun
```

서버는 `http://localhost:8080` 에서 실행됩니다.

## 📊 ERD 및 API 명세
![회원가입](screenshots/프로젝트ERD관계도.png)

### 📡 API 엔드포인트 정리

#### 1️⃣ Member API (회원 관리)

**인증**
- `POST /members` - 회원가입
- `GET /members/login` - 로그인
- `GET /members/{memId}` - 회원 상세정보 조회

**중복검사**
- `GET /members/checkId/{memId}` - 아이디 중복검사
- `GET /members/checkTell/{memTell}` - 연락처 중복검사
- `GET /members/checkBusinessNum/{memBusinessNum}` - 사업자번호 중복검사

**회원정보 관리**
- `PUT /members/{memId}` - 회원정보 수정
- `PUT /members/{memId}/withdraw` - 회원 탈퇴
- `GET /members/findId` - 아이디 찾기
- `GET /members/findPw` - 비밀번호 찾기

**프로필 이미지**
- `POST /members/profile-image` - 프로필 이미지 업로드 (JPG/JPEG/PNG, 최대 10MB)
- `GET /members/profile-image/{memId}` - 프로필 이미지 조회

**관리자 기능**
- `GET /members/admin` - 전체 활성 회원 목록
- `GET /members/admin/deleted` - 삭제/탈퇴 회원 목록
- `GET /members/status/{memId}` - 회원 상태 확인
- `PUT /members/admin/{memId}/delete` - 회원 삭제
- `PUT /members/admin/{memId}/restore` - 회원 복구

---

#### 2️⃣ Board API (게시판)

**게시글 CRUD**
- `POST /boards` - 게시글 등록
- `GET /boards/{memId}` - 마이팜 게시글 조회
- `GET /boards/boardList-paging` - 페이징 목록 조회
- `GET /boards/boardDetail/{boardNum}` - 게시글 상세 조회 (조회수 자동 증가)
- `PUT /boards/boardDetail/{boardNum}` - 게시글 수정
- `DELETE /boards/boardDetail/{boardNum}` - 게시글 삭제 (사용자)
- `DELETE /boards/{boardNum}` - 게시글 삭제 (관리자)

**특수 조회**
- `GET /boards` - 홈화면 인기글 조회
- `GET /boards/boardList` - 전체 게시글 조회

**이미지 관리**
- `POST /boards/upload/img` - 게시글 작성 시 이미지 미리 등록 (MultipartFile)

---

#### 3️⃣ Chat API (실시간 채팅)

**채팅방 관리**
- `POST /api/chat/room/direct` - 1:1 채팅방 생성 (memId1, memId2 필수)
- `POST /api/chat/room/group` - 단체 채팅방 생성 (roomName, memberIds 필수)
- `GET /api/chat/room/{roomId}` - 채팅방 조회
- `GET /api/chat/rooms/{memId}` - 내 채팅방 목록

**메시지 관리**
- `POST /api/chat/message` - 메시지 전송
- `GET /api/chat/messages/{roomId}` - 메시지 목록 (페이징: page, size)
- `DELETE /api/chat/message/{msgId}` - 메시지 삭제
- `GET /api/chat/unread/{memId}/{roomId}` - 안 읽은 메시지 수

**참여자 관리**
- `POST /api/chat/room/{roomId}/participant/{memId}` - 참여자 추가
- `GET /api/chat/room/{roomId}/participants` - 참여자 목록
- `DELETE /api/chat/room/{roomId}/leave/{memId}` - 채팅방 나가기

**읽음 처리 & 파일**
- `PUT /api/chat/room/{roomId}/read/{memId}` - 메시지 읽음 표시
- `POST /api/chat/upload` - 채팅 파일 업로드 (file, roomId, senderId 필수)

---

#### 4️⃣ Weather API (날씨)

**좌표 변환**
- `GET /api/weather/geocode` - 주소를 좌표로 변환 (Kakao API 활용)

---

### 주요 테이블
- `member`: 회원 정보
- `board`: 게시글
- `comment`: 댓글
- `plant`: 식물 정보
- `calendar`: 일정 관리
- `chat_room`: 채팅방
- `message`: 메시지/알림
- `follow`: 팔로우 관계
- `board_like`: 좋아요

## 🎯 핵심 기능 시연

### 1️⃣ 메인 화면
> 직관적인 UI/UX로 식물 커뮤니티의 모든 기능에 쉽게 접근

![메인화면](screenshots/홈화면.PNG)
<!-- 또는 GIF: ![메인화면](screenshots/main.gif) -->

**구현 기술**
- RESTful API를 통한 데이터 페칭
- 반응형 레이아웃 설계
- 최신 게시글, 인기 게시글 실시간 업데이트

**주요 기능**
- 📊 대시보드 형태의 정보 표시
- 🔍 통합 검색 기능
- 🎨 카테고리별 필터링
- ⚡ 빠른 네비게이션

---

### 2️⃣ 회원가입 및 로그인
> 안전하고 편리한 사용자 인증 시스템

![회원가입](screenshots/회원가입.png)
![아이디,비번찾기](screenshots/아이디,비밀번호 찾기.png)
![회원정보수정](screenshots/회원정보수정.png)

**구현 기술**
- Spring Boot 기반* *세션 관리
- 비밀번호 암호화 (BCrypt 예정)
- 유효성 검증 (Validation)
- MyBatis를 활용한 회원 정보 관리

**주요 기능**
- ✅ 실시간 중복 확인 (아이디, 이메일)
- 🔒 안전한 비밀번호 정책
- 📧 이메일 형식 검증
- 🎭 프로필 이미지 업로드

**API 엔드포인트**
```java
POST /api/members/signup    // 회원가입
POST /api/members/login      // 로그인
GET  /api/members/check      // 중복 확인
POST /api/members/logout     // 로그아웃
```

---

### 3️⃣ 실시간 채팅
> WebSocket STOMP 프로토콜 기반의 실시간 양방향 통신

![쪽지보내기](screenshots/쪽지보내기.PNG)
![쪽지세부사항](screenshots/쪽지세부사항.PNG)
![쪽지답장](screenshots/쪽지답장.PNG)

**구현 기술**
- **WebSocket + STOMP**: 실시간 메시지 전송/수신
- **SockJS**: WebSocket을 지원하지 않는 브라우저 대응
- **메시지 브로커**: 효율적인 메시지 라우팅
- **MyBatis**: 채팅 내역 영구 저장

**핵심 구현 코드**
```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {
    @Override
    public void configureMessageBroker(MessageBrokerRegistry config) {
        config.enableSimpleBroker("/topic", "/queue");
        config.setApplicationDestinationPrefixes("/app");
    }
    
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/ws")
                .setAllowedOriginPatterns("*")
                .withSockJS();
    }
}
```

**주요 기능**
- 💬 1:1 개인 채팅
- 👥 그룹 채팅방 생성
- ✅ 메시지 읽음 처리
- 🟢 실시간 접속 상태 표시
- 📎 파일 및 이미지 전송
- ⏰ 메시지 타임스탬프
- 🔔 새 메시지 알림

**메시지 흐름**
```
Client ─────> STOMP ─────> Message Broker ─────> Subscribers
   └─ Send      └─ /app/chat    └─ /topic/messages    └─ Receive
```

**실시간 통신 프로세스**
1. 클라이언트가 WebSocket 연결 수립
2. STOMP 프로토콜로 채팅방 구독 (/topic/chat/{roomId})
3. 메시지 발송 (/app/chat/send)
4. 서버에서 메시지 처리 및 DB 저장
5. 구독자들에게 실시간 브로드캐스트

---

### 4️⃣ 식물 도감, 환경데이터
> 다양한 식물 정보를 제공하는 백과사전

![식물정보, 작동로그](screenshots/식물선택,작동로그.png)
![환경그래프](screenshots/환경그래프.png)

**구현 기술**
- RESTful API 설계
- 페이지네이션 처리
- 검색 및 필터링 최적화
- 이미지 최적화 및 로딩

**주요 기능**
- 🔍 식물명 검색 (한글, 학명)
- 📑 카테고리별 분류
    - 관엽식물
    - 다육식물
    - 허브
    - 꽃식물
- 📊 난이도별 필터 (초급/중급/고급)
- 💧 물주기 정보
- ☀️ 햇빛 요구량
- 🌡️ 적정 온도/습도
- ⭐ 사용자 평점 및 리뷰
- 📚 상세 재배 가이드

**API 엔드포인트**
```java
GET  /api/plants              // 식물 목록 조회
GET  /api/plants/{id}         // 식물 상세 조회
GET  /api/plants/search       // 식물 검색
GET  /api/plants/category     // 카테고리별 조회
POST /api/plants/{id}/review  // 리뷰 작성
```

**데이터 구조**
```java
//식물 정보 테이블 생성
CREATE TABLE CROP_STANDARDS(
  HERB_NUM INT PRIMARY KEY AUTO_INCREMENT, #작물 ID
  HERB_NAME VARCHAR(50) NOT NULL, #작물 이름
  TEMP_MIN FLOAT NOT NULL, #최저 온도
  TEMP_MAX FLOAT NOT NULL, #최대 온도
  HUMID_MIN FLOAT NOT NULL, #최저 습도
  HUMID_MAX FLOAT NOT NULL, #최대 습도
  SOIL_MIN FLOAT NOT NULL, #최소 토양 수분
  SOIL_MAX FLOAT NOT NULL, #최대 토양 수분
  LUX_MIN INT NOT NULL, #최소 조도
  LUX_MAX INT NOT NULL, #최대 조도
  IMG_NAME VARCHAR(100) NOT NULL #작물 이미지
);

//식물 데이터 삽입
INSERT INTO CROP_STANDARDS	(
  HERB_NAME, TEMP_MIN, TEMP_MAX, HUMID_MIN, HUMID_MAX
  , SOIL_MIN, SOIL_MAX, LUX_MIN, LUX_MAX, IMG_NAME
  ) VALUES(
  '바질', 20, 30, 40, 60, 25, 40, 20000, 60000, '바질.jfjf'),
  ('로즈마리', 15, 25, 30, 50, 10, 20, 30000, 70000, '로즈마리.jfjf'),
  ('라벤더', 15, 25, 30, 50, 10, 20, 30000, 70000, '라벤더.jfjf'),
  ('민트', 15, 25, 50, 70, 30, 45, 15000, 40000, '민트.jfjf'),
  ('타임', 15, 25, 30, 50, 10, 20, 20000, 60000, '타임.jfjf'),
  ('파슬리', 15, 25, 40, 60, 20, 35, 15000, 40000, '파슬리.jfjf'
);
```

---

## 💡 기술적 구현 포인트

### WebSocket 실시간 통신
```java
@MessageMapping("/chat/send")
@SendTo("/topic/messages")
public ChatMessageDTO sendMessage(ChatMessageDTO message) {
    // 메시지 DB 저장
    chatService.saveMessage(message);
    // 실시간 브로드캐스트
    return message;
}
```

### 세션 기반 인증
```java
@PostMapping("/login")
public ResponseEntity<?> login(@RequestBody LoginDTO dto, HttpSession session) {
    Member member = memberService.authenticate(dto);
    if (member != null) {
        session.setAttribute("loginMember", member);
        return ResponseEntity.ok().build();
    }
    return ResponseEntity.status(401).build();
}
```

### 페이지네이션 처리
```java
@GetMapping("/plants")
public ResponseEntity<PageResponseDTO<PlantDTO>> getPlants(
    @RequestParam(defaultValue = "1") int page,
    @RequestParam(defaultValue = "12") int size) {
    
    PageRequestDTO pageRequest = new PageRequestDTO(page, size);
    PageResponseDTO<PlantDTO> response = plantService.getPlantList(pageRequest);
    return ResponseEntity.ok(response);
}
```

## 🔧 개선 및 확장 계획

- [ ] Spring Security 적용한 인증/인가 시스템
- [ ] Redis 캐싱 도입으로 성능 최적화
- [ ] 알림 기능 고도화 (FCM 연동)
- [ ] 식물 AI 진단 기능

## 📝 개발 환경

- **IDE**: IntelliJ IDEA
- **Build Tool**: Gradle
- **Version Control**: Git
- **API Test**: Postman

## 👥 팀 구성

- **Frontend Developer - Web**: [유지수]
- **Frontend Developer - App**: [유지수]
- **Backend Developer**: [유지수]


## 📧 연락처

- Email: yoo901013@gmail.com
- GitHub: [@yoojisu90](https://github.com/yoojisu90)
- Portfolio: [your-portfolio-link](https://your-portfolio.com)

---

⭐ 이 프로젝트가 마음에 드신다면 스타를 눌러주세요!