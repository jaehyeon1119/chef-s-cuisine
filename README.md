# Chef's Cuisine - 레시피 공유 웹서비스

> React와 Spring Boot를 기반으로 사용자가 레시피를 검색·등록·공유하고, 댓글·좋아요·알림·마이페이지 기능을 통해 상호작용할 수 있도록 구현한 커뮤니티형 레시피 공유 웹서비스입니다.

## 프로젝트 개요

| 구분 | 내용 |
|---|---|
| 프로젝트명 | Chef's Cuisine |
| 프로젝트 유형 | 팀 프로젝트 / 레시피 공유 웹서비스 |
| 개발 기간 | 2026.05.27 ~ 2026.06.30 |
| 담당 역할 | 팀장, 일정·협업 관리, 알림 기능, 마이페이지 게시판, 일부 마이페이지 기능 연동 |
| GitHub | https://github.com/jaehyeon1119/chef-s-cuisine |
| 배포 | AWS EC2 기반 배포 |

Chef's Cuisine은 사용자가 레시피를 쉽고 편리하게 검색하고 공유할 수 있도록 만든 웹서비스입니다.  
레시피 등록, 이미지 업로드, 레시피 검색, 상세 조회, 후기, 좋아요, 마이페이지, 구독, 방명록, 알림 기능을 구현했으며, 관리자 기능과 Gemini API 기반 레시피 설명·칼로리 생성 기능도 포함했습니다.

## 팀 구성 및 담당 역할

| 이름 | 역할 | 담당 업무 |
|---|---|---|
| 이재현 | 팀장 | 일정 관리, 역할 분담, 알림 기능, 마이페이지 게시판, GitHub 협업 관리 |
| 궁주영 | 팀원 | DB 설계, 배포, AI 기능, 레시피 CRUD, 관리자 기능 |
| 정민기 | 팀원 | 요구사항 정의, 회원 기능, 검색 기능 |
| 공통 | 공동 | 프로젝트 기획, 데이터 입력, 테스트 및 디버깅, 협업 관리 |

### 나의 주요 담당 업무

- 팀장으로 프로젝트 주제 선정, 역할 분담, 일정 계획 수립 및 진행 상황 점검
- GitHub 브랜치 작업물 확인, 충돌 발생 시 파일 비교 및 병합
- 알림 기능 구현
  - 알림 목록 조회
  - 읽음 처리
  - 전체 읽음 처리
  - 알림 ON/OFF 처리
  - 알림 타입별 화면 이동 처리
- 마이페이지 게시판 기능 구현
  - 게시글 작성, 수정, 삭제
  - 이미지 최대 5장 업로드
  - 댓글 작성, 수정, 삭제
  - 좋아요 기능
  - 페이지네이션 및 정렬
- 게시판 댓글/좋아요 발생 시 NotificationService와 연동하여 알림 데이터 생성
- 마이페이지 사용자 활동 영역과 게시판 탭 연결 및 화면 흐름 테스트

## 개발 환경

### Front-end

| 구분 | 기술 |
|---|---|
| Framework | React 19 |
| Build Tool | Vite |
| Language | TypeScript, JavaScript |
| Routing | React Router |
| HTTP Client | Axios |
| UI | CSS, Tailwind CSS, lucide-react, react-icons |

### Back-end

| 구분 | 기술 |
|---|---|
| Framework | Spring Boot 3.2.5 |
| Language | Java 17 |
| Persistence | MyBatis 3.0.5 |
| Build Tool | Gradle |
| Security | Spring Security |
| File Upload | MultipartFile, AWS S3 |

### Database / Infra

| 구분 | 기술 |
|---|---|
| Database | MySQL 8.0 |
| File Storage | AWS S3 |
| Deploy | AWS EC2 |
| CI/CD Test | GitHub Actions AWS Connection Test |
| Collaboration | GitHub |
| Tools | VS Code, Eclipse, DBeaver, Postman |

## 프로젝트 구조

```text
chef-s-cuisine/
├── semifront/                    # React + Vite 프론트엔드
│   ├── src/
│   │   ├── api/                  # Axios 공통 인스턴스
│   │   ├── components/           # 화면 컴포넌트
│   │   │   ├── mypage/           # 마이페이지 탭 기능
│   │   │   ├── Layout.tsx        # 공통 레이아웃 및 알림 UI
│   │   │   ├── RecipeBrowse.tsx  # 레시피 검색/목록
│   │   │   ├── RecipeDetail.tsx  # 레시피 상세
│   │   │   ├── RecipeWrite.tsx   # 레시피 등록
│   │   │   └── TopChef.tsx       # 홈스토랑/Top Chef
│   │   ├── config/               # API, 이미지 base URL 설정
│   │   ├── service/              # API 호출 서비스
│   │   ├── types/                # 공통 타입
│   │   └── utils/                # 날짜, 좋아요 유틸
│   └── package.json
│
├── semiproject/                  # Spring Boot 백엔드
│   ├── src/main/java/org/cloud/
│   │   ├── configuration/        # DB, Security, Web MVC 설정
│   │   ├── control/              # Controller 계층
│   │   ├── dto/                  # DTO
│   │   ├── mapper/               # MyBatis Mapper Interface
│   │   └── service/              # Business Logic
│   ├── src/main/resources/
│   │   ├── mapper/               # MyBatis XML SQL
│   │   └── application.properties
│   ├── Dockerfile
│   └── build.gradle
│
└── .github/workflows/            # GitHub Actions 설정
```

## 주요 기능

### 1. 회원 / 인증 기능

- 회원가입 및 로그인
- 로그인 사용자 기준 PrivateRoute 처리
- 회원 정보 조회 및 수정
- 프로필 이미지 등록
- 자기소개, SNS 링크 수정
- 스크랩 레시피 공개 여부 ON/OFF
- 회원 탈퇴 기능

### 2. 레시피 기능

- 레시피 목록 조회
- 레시피 상세 조회
- 레시피 등록, 수정, 삭제
- 대표 이미지 및 조리 단계 이미지 업로드
- 재료, 조리순서, 태그, 유튜브 영상 링크 관리
- 조회 수 증가 처리
- 좋아요 및 스크랩 레시피 조회
- 후기 등록 및 후기 이미지 조회

### 3. 레시피 검색 기능

레시피 목록 화면에서 다양한 조건을 조합하여 검색할 수 있도록 구현했습니다.

- 레시피명 검색
- 회원명 검색
- 태그 검색
- 재료 검색
- 난이도 검색
- 조리시간 검색
- 최신순, 좋아요순, 조회순, 인기순 정렬
- 페이지네이션

검색 조건은 프론트엔드에서 URLSearchParams로 관리하고, 백엔드에서는 RecipeSearchParams DTO와 MyBatis 동적 SQL을 사용해 조건이 있을 때만 SQL 조건이 적용되도록 구현했습니다.

### 4. 마이페이지 기능

- 사용자 프로필 조회
- 프로필 배경 이미지 슬라이드
- 작성 레시피 조회
- 스크랩 레시피 조회
- 마이페이지 게시판
- 구독 목록 조회
- 방명록 작성 및 조회
- 내 정보 수정
- 회원 탈퇴 확인

마이페이지는 `mypage/:userId?` 선택적 파라미터를 사용하여 내 페이지와 타인 페이지를 함께 처리했습니다.  
게시판, 작성 레시피, 스크랩 레시피, 구독, 방명록 기능을 탭별 컴포넌트로 분리하여 유지보수성을 높였습니다.

### 5. 마이페이지 게시판 기능

- 게시글 작성, 수정, 삭제
- 이미지 최대 5장 업로드
- 댓글 작성, 수정, 삭제
- 게시글 좋아요
- 최신순 정렬
- 페이지네이션
- 작성자 또는 관리자만 삭제 가능하도록 권한 검증
- 게시글 삭제 시 좋아요, 댓글을 먼저 삭제한 뒤 게시글 삭제 처리

게시글 이미지는 프론트엔드에서 FormData로 전송하고, 백엔드에서 MultipartFile 목록을 받아 파일 개수를 한 번 더 검증했습니다.  
삭제 시에는 FK 제약을 고려하여 좋아요, 댓글, 게시글 순서로 삭제되도록 처리했습니다.

### 6. 알림 기능

- 헤더 알림 아이콘 표시
- 읽지 않은 알림 목록 조회
- 알림 개수 배지 표시
- 알림 개별 읽음 처리
- 전체 읽음 처리
- 알림 ON/OFF 처리
- 알림 타입별 화면 이동
  - 레시피 좋아요 / 레시피 댓글 → 레시피 상세 페이지
  - 게시판 댓글 / 게시판 좋아요 → 마이페이지
  - 방명록 / 구독 → 마이페이지

알림 생성 시 `receiverId`와 `senderId`가 같은 경우 알림을 생성하지 않도록 검증하여, 자기 자신이 작성한 댓글이나 좋아요에는 알림이 발생하지 않도록 처리했습니다.

### 7. 홈스토랑 / Top Chef 기능

- 카테고리별 Chef 목록 조회
- 선택한 Chef의 회원 정보 조회
- 선택한 Chef가 작성한 레시피 목록 조회
- 레시피 대표 이미지를 활용한 배너 슬라이드
- 레시피별 좋아요 상태 적용
- 정렬 및 카드형 UI 구성

### 8. 관리자 / AI 기능

- 관리자 데이터 관리
- 공공데이터 기반 레시피 데이터 초기화
- Gemini API 기반 레시피 소개 생성
- Gemini API 기반 칼로리 생성

## 주요 API

| 기능 | Method | Endpoint | 설명 |
|---|---|---|---|
| 회원가입 | POST | `/api/member/register` | 회원 정보 등록 |
| 로그인 | POST | `/api/member/login` | 로그인 처리 |
| 로그아웃 | POST | `/api/member/logout` | 로그아웃 처리 |
| 레시피 목록 | GET | `/api/recipe/list` | 레시피 목록 조회 |
| 레시피 검색 | GET | `/api/recipe/browse` | 조건별 레시피 검색 |
| 레시피 상세 | GET | `/api/recipe/{recipeId}` | 레시피 상세 조회 |
| 레시피 등록 | POST | `/api/recipe/register` | 레시피 기본정보, 재료, 조리순서, 태그 등록 |
| 레시피 이미지 업로드 | POST | `/api/recipe-images/{recipeCode}/upload` | 대표 이미지 업로드 |
| 조리 단계 이미지 업로드 | POST | `/api/recipe-images/step-image` | 조리순서 이미지 업로드 |
| 좋아요 토글 | POST | `/api/like/toggle` | 레시피 좋아요/취소 |
| 마이페이지 작성 레시피 | GET | `/api/recipe/by-writer/{writerId}` | 작성자 기준 레시피 조회 |
| 스크랩 레시피 | GET | `/api/like/my-recipes/{userId}` | 사용자가 좋아요한 레시피 조회 |
| 게시글 목록 | GET | `/api/posts` | 마이페이지 게시글 목록 조회 |
| 게시글 작성 | POST | `/api/posts` | 이미지 포함 게시글 작성 |
| 게시글 수정 | PUT | `/api/posts/{postId}` | 게시글 수정 |
| 게시글 삭제 | DELETE | `/api/posts/{postId}` | 게시글 삭제 |
| 댓글 작성 | POST | `/api/posts/comment` | 게시글 댓글 작성 |
| 댓글 수정 | PUT | `/api/posts/comment/{commentId}` | 댓글 수정 |
| 댓글 삭제 | DELETE | `/api/posts/comment/{commentId}` | 댓글 삭제 |
| 게시글 좋아요 | POST | `/api/posts/{postId}/like` | 게시글 좋아요/취소 |
| 알림 목록 | GET | `/api/notifications/{receiverId}` | 읽지 않은 알림 조회 |
| 알림 개수 | GET | `/api/notifications/{receiverId}/unread-count` | 읽지 않은 알림 개수 조회 |
| 알림 읽음 | PUT | `/api/notifications/{notiId}/read` | 단건 읽음 처리 |
| 전체 읽음 | PUT | `/api/notifications/{receiverId}/read-all` | 전체 읽음 처리 |
| 구독 | POST | `/api/social/follow` | 사용자 구독 |
| 구독 취소 | DELETE | `/api/social/unfollow` | 사용자 구독 취소 |
| 구독 목록 | GET | `/api/social/following/{userId}` | 구독 중인 회원 목록 조회 |
| 방명록 조회 | GET | `/api/guestbook/{hostId}` | 방명록 목록 조회 |
| 방명록 작성 | POST | `/api/guestbook` | 방명록 작성 |
| AI 요청 | POST | `/api/ai/chat` | Gemini API 기반 텍스트 생성 |

## 핵심 구현 포인트

### 알림 중복 및 자기 알림 방지

댓글 또는 좋아요 이벤트 발생 시 알림을 생성하되, 작성자와 이벤트 발생자가 같은 경우에는 알림을 생성하지 않도록 처리했습니다.

```java
if (receiverId == null || receiverId.isBlank()) return false;
if (senderId == null || senderId.isBlank()) return false;
if (receiverId.equals(senderId)) return false;
```

### 게시판 이미지 업로드 개수 제한

프론트엔드와 백엔드에서 모두 이미지 개수를 검증하여 최대 5장까지만 업로드할 수 있도록 처리했습니다.

```java
if (uploadImages.size() > 5) {
    throw new IllegalArgumentException("게시판 사진은 최대 5장까지 등록 가능합니다.");
}
```

### 레시피 검색 동적 SQL

검색어, 태그, 재료, 난이도, 조리시간 등 조건이 있을 때만 SQL 조건이 추가되도록 MyBatis 동적 SQL을 적용했습니다.

```xml
<if test="recipeNmKo != null and recipeNmKo != ''">
    AND r.recipe_nm_ko LIKE CONCAT('%', #{recipeNmKo}, '%')
</if>
```

### 레시피 등록 흐름

레시피 등록 시 기본정보, 재료, 조리순서, 작성자, 태그를 하나의 payload로 묶어 저장하고, 대표 이미지는 레시피 등록 후 반환받은 `recipeCode`를 기준으로 별도 업로드했습니다.

```ts
const response = await api.post("/recipe/register", recipePayload);
const recipeCode = response.data;

if (mainImages.length > 0 && recipeCode) {
  const formData = new FormData();
  mainImages.forEach((file) => formData.append("files", file));
  await api.post(`/recipe-images/${recipeCode}/upload`, formData);
}
```

## 실행 방법

### 1. Backend 실행

```bash
cd semiproject
```

필요한 환경변수를 설정합니다.

```bash
DB_PASSWORD=본인_DB_비밀번호
RECIPE_API_KEY=공공데이터_API_KEY
GEMINI_API_KEY=Gemini_API_KEY
S3_BUCKET_NAME=사용할_S3_BUCKET_NAME
```

실행합니다.

```bash
./gradlew bootRun
```

Windows 환경에서는 다음 명령어를 사용할 수 있습니다.

```bash
gradlew.bat bootRun
```

### 2. Frontend 실행

```bash
cd semifront
npm install
npm run dev
```

프론트엔드 API 주소는 `.env` 파일에서 설정할 수 있습니다.

```env
VITE_API_BASE_URL=http://localhost:8080
VITE_IMG_BASE_URL=http://localhost:8080
```

배포 환경에서는 EC2 서버 주소 또는 S3 이미지 주소에 맞게 변경합니다.

## 산출물

프로젝트 제출 자료에는 다음 산출물이 포함되어 있습니다.

- 프로젝트 기획 자료
  - 주제 선정 및 참고사이트
  - 프로젝트 일정 계획표
  - 간트차트
- 프로젝트 설계 자료
  - ERD / DB 설계
  - Backend 구조
  - Frontend 구조
  - 메뉴 구성 및 메인페이지 설계
- 기능 구현 캡처
  - 로그인 / 회원가입
  - 레시피 검색 / 등록 / 상세
  - 마이페이지 / 게시판 / 방명록 / 구독
  - 알림 기능
  - 홈스토랑 / Top Chef
  - 관리자 / AI 기능
- 구현 자료
  - AWS 인스턴스 생성 캡처
  - 개발환경 캡처
  - 시연 영상
  - 프로젝트 결과보고서 PPT
  - 포트폴리오 PDF

## 트러블슈팅 및 개선 경험

### 1. 알림 생성 조건 오류

댓글 또는 좋아요 발생 시 자기 자신에게도 알림이 생성될 수 있는 문제가 있었습니다.  
`receiverId`와 `senderId`를 비교하여 같은 경우 알림을 생성하지 않도록 처리했습니다.

### 2. 게시글 삭제 시 FK 제약 문제

게시글 삭제 시 댓글과 좋아요 데이터가 남아 있으면 삭제가 실패할 수 있었습니다.  
좋아요, 댓글, 게시글 순서로 삭제되도록 처리하여 데이터 무결성을 고려했습니다.

### 3. 이미지 업로드 개수 제한

프론트엔드에서만 이미지 개수를 제한하면 우회 가능성이 있어 백엔드에서도 MultipartFile 개수를 검증하도록 구현했습니다.

### 4. 검색 조건 증가에 따른 SQL 복잡도 증가

검색 조건이 많아지면서 SQL이 복잡해졌습니다.  
검색 조건을 DTO로 관리하고 MyBatis 동적 SQL을 적용하여 조건별 검색과 정렬을 안정적으로 처리했습니다.

### 5. 배포 환경 설정

DB 비밀번호, 공공데이터 API Key, Gemini API Key, S3 Bucket 이름 등 민감정보는 환경변수로 분리하여 관리하도록 구성했습니다.

## 보안상 주의사항

- `application.properties`에서는 민감정보를 직접 작성하지 않고 환경변수로 주입합니다.
- GitHub에 DB 비밀번호, API Key, AWS Key, 토큰 값을 직접 업로드하지 않습니다.
- 포트폴리오 캡처에 `password`, `token`, `secret`, `key` 값이 보이는 경우 반드시 마스킹 처리합니다.
- 배포 환경에서는 CORS 허용 주소를 필요한 도메인으로만 제한합니다.

## 프로젝트를 통해 배운 점

이번 프로젝트를 통해 React와 Spring Boot를 REST API로 연결하고, MyBatis를 통해 MySQL 데이터를 처리하는 전체 흐름을 경험했습니다.  
특히 알림 기능과 게시판 기능은 사용자 이벤트, API 호출, DB 저장, 화면 갱신이 모두 연결되어 있어 오류를 찾는 과정이 쉽지 않았지만, 브라우저 콘솔, 네트워크 요청, 서버 로그, SQL 결과를 차례대로 확인하며 문제를 해결했습니다.

팀장으로서 일정 계획, 역할 분담, GitHub 협업 관리, 충돌 해결, 테스트 진행 상황 점검까지 함께 경험하며 단순 기능 구현뿐 아니라 팀 프로젝트의 전체 흐름을 관리하는 역량을 키울 수 있었습니다.
