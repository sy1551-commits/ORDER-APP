# 📁 프로젝트 구조

## 프로젝트 개요
**COZY 커피 주문 앱** - 사용자가 커피를 주문하고 관리자가 주문을 관리할 수 있는 풀스택 웹 애플리케이션

---

## 📂 전체 폴더 구조

```
ORDER-APP/
├── docs/                          # 프로젝트 문서
│   ├── PRD.md                    # 제품 요구사항 문서
│   └── project_structure.md      # 프로젝트 구조 문서 (현재 파일)
│
├── server/                        # 백엔드 애플리케이션
│   ├── config/                   # 설정 파일
│   │   ├── database.js          # 데이터베이스 연결 설정
│   │   └── schema.sql           # 데이터베이스 스키마 정의
│   ├── controllers/              # 비즈니스 로직 컨트롤러
│   │   ├── inventoryController.js  # 재고 관리 로직
│   │   ├── menuController.js       # 메뉴 관리 로직
│   │   └── orderController.js      # 주문 관리 로직
│   ├── models/                   # 데이터 모델
│   │   ├── Menu.js              # 메뉴 데이터 모델
│   │   └── Order.js             # 주문 데이터 모델
│   ├── routes/                   # API 라우트
│   │   ├── admin.js             # 관리자 API 라우트
│   │   ├── inventory.js         # 재고 API 라우트
│   │   ├── menus.js             # 메뉴 API 라우트
│   │   └── orders.js            # 주문 API 라우트
│   ├── app.js                    # Express 서버 진입점
│   ├── config.js                 # 환경 설정
│   ├── init-db.js                # 데이터베이스 초기화 스크립트
│   ├── clean-db.js               # 데이터베이스 정리 스크립트
│   ├── database.sqlite           # SQLite 데이터베이스 파일 (개발용)
│   ├── package.json              # 백엔드 의존성 관리
│   └── README.md                 # 백엔드 설명서
│
├── ui/                            # 프론트엔드 애플리케이션
│   ├── public/                   # 정적 파일
│   │   ├── images/              # 커피 이미지
│   │   │   ├── americano-hot.jpg
│   │   │   ├── americano-ice.jpg
│   │   │   └── cafe-latte.jpg
│   │   ├── _redirects           # SPA 라우팅 설정 (배포용)
│   │   ├── iced-coffee-7113043_1920.jpg
│   │   └── vite.svg
│   ├── src/                      # 소스 코드
│   │   ├── assets/              # 정적 리소스
│   │   │   └── react.svg
│   │   ├── App.jsx              # 메인 React 컴포넌트
│   │   ├── App.css              # 앱 스타일
│   │   ├── main.jsx             # React 진입점
│   │   └── index.css            # 전역 스타일
│   ├── dist/                     # 빌드 결과물 (배포용)
│   ├── eslint.config.js          # ESLint 설정
│   ├── vite.config.js            # Vite 빌드 설정
│   ├── package.json              # 프론트엔드 의존성 관리
│   └── README.md                 # 프론트엔드 설명서
│
├── DEPLOYMENT.md                  # 배포 가이드 (Render.com)
└── *.jpg                          # 프로젝트 이미지 파일들

```

---

## 🖥️ 백엔드 (server/)

### 📌 주요 파일 설명

#### **app.js**
- Express 서버의 진입점
- 미들웨어 설정 (CORS, JSON 파싱)
- API 라우트 등록
- 서버 시작 및 데이터베이스 연결

#### **config.js**
- 환경 변수 관리
- 데이터베이스 타입 (SQLite/PostgreSQL) 설정
- 포트, CORS 등 서버 설정

### 📁 config/ - 데이터베이스 설정

#### **database.js**
- SQLite와 PostgreSQL 연결 관리
- 환경에 따른 데이터베이스 선택
- 쿼리 실행 헬퍼 함수

#### **schema.sql**
- 데이터베이스 테이블 정의
- 테이블: menus, options, orders, order_items, order_item_options
- 초기 데이터 삽입 쿼리

### 📁 controllers/ - 비즈니스 로직

#### **menuController.js**
- 메뉴 조회 로직
- 메뉴별 옵션 조회
- 활성화된 메뉴 필터링

#### **orderController.js**
- 주문 생성 및 조회
- 주문 상태 변경 (주문 접수 → 제조 중 → 제조 완료)
- 주문 통계 계산

#### **inventoryController.js**
- 재고 현황 조회
- 재고 수량 조정 (+/-)
- 재고 부족 알림

### 📁 models/ - 데이터 모델

#### **Menu.js**
- 메뉴 데이터 CRUD 작업
- 메뉴-옵션 관계 처리
- 재고 관리 쿼리

#### **Order.js**
- 주문 데이터 CRUD 작업
- 주문 아이템 및 옵션 처리
- 주문 상태 업데이트

### 📁 routes/ - API 라우트

#### **menus.js**
- `GET /api/menus` - 메뉴 목록 조회
- `GET /api/menus/:id/options` - 메뉴별 옵션 조회

#### **orders.js**
- `POST /api/orders` - 주문 생성
- `GET /api/orders` - 주문 목록 조회
- `PUT /api/orders/:id/status` - 주문 상태 변경

#### **inventory.js**
- `GET /api/inventory` - 재고 현황 조회
- `PUT /api/inventory/:id` - 재고 수량 변경

#### **admin.js**
- `GET /api/admin/stats` - 관리자 통계 조회
- 기타 관리자 전용 API

### 🛠️ 유틸리티 스크립트

#### **init-db.js**
- 데이터베이스 초기화
- 테이블 생성
- 초기 데이터 삽입

#### **clean-db.js**
- 데이터베이스 정리
- 테스트 데이터 삭제

---

## 🎨 프론트엔드 (ui/)

### 📌 주요 파일 설명

#### **main.jsx**
- React 애플리케이션 진입점
- React DOM 렌더링
- StrictMode 설정

#### **App.jsx**
- 메인 컴포넌트
- 주문하기 / 관리자 화면 전환
- 상태 관리 (장바구니, 메뉴, 주문)
- API 통신 로직

#### **App.css**
- 전체 앱 스타일
- 컴포넌트별 스타일 정의
- 반응형 디자인 (모바일, 태블릿, 데스크톱)

#### **index.css**
- 전역 스타일
- CSS 리셋
- 공통 변수 및 유틸리티 클래스

### 📁 public/ - 정적 파일

#### **images/**
- 커피 메뉴 이미지
- americano-hot.jpg, americano-ice.jpg, cafe-latte.jpg

#### **_redirects**
- SPA(Single Page Application) 라우팅 설정
- Render.com 배포용 리다이렉트 규칙

### 📁 dist/ - 빌드 결과물

- Vite 빌드 후 생성되는 폴더
- 최적화된 HTML, CSS, JavaScript
- 배포 시 이 폴더를 사용

### ⚙️ 설정 파일

#### **vite.config.js**
- Vite 빌드 도구 설정
- React 플러그인 설정
- 개발 서버 설정

#### **eslint.config.js**
- JavaScript 코드 품질 검사
- React 규칙 적용

#### **package.json**
- 프로젝트 의존성 (React, React-DOM, Vite)
- 스크립트 명령어 (dev, build, preview)

---

## 🗄️ 데이터베이스 구조

### 테이블 구조

#### **menus**
- 커피 메뉴 정보
- 필드: id, name, description, base_price, image, stock, is_active

#### **options**
- 메뉴별 옵션 (샷 추가, 시럽 추가 등)
- 필드: id, name, price

#### **orders**
- 주문 정보
- 필드: id, order_number, order_time, status, total_amount

#### **order_items**
- 주문별 상품 목록
- 필드: id, order_id, menu_id, quantity, base_price, item_total

#### **order_item_options**
- 주문 상품별 선택 옵션
- 필드: id, order_item_id, option_id, option_name, option_price

---

## 🔄 데이터 흐름

### 주문 프로세스
1. **사용자**: 메뉴 선택 및 옵션 선택
2. **프론트엔드**: 장바구니에 추가
3. **API 요청**: `POST /api/orders`
4. **백엔드**: 주문 생성 및 재고 차감
5. **데이터베이스**: orders, order_items, order_item_options 테이블에 저장
6. **응답**: 주문 완료 알림

### 관리자 프로세스
1. **관리자**: 관리자 화면 접속
2. **API 요청**: `GET /api/orders`, `GET /api/inventory`
3. **백엔드**: 주문 목록 및 재고 정보 조회
4. **주문 처리**: 상태 변경 (`PUT /api/orders/:id/status`)
5. **재고 관리**: 재고 조정 (`PUT /api/inventory/:id`)

---

## 🚀 실행 방법

### 개발 환경

#### 백엔드 실행
```bash
cd server
npm install
npm run dev
```
- 서버: http://localhost:3001

#### 프론트엔드 실행
```bash
cd ui
npm install
npm run dev
```
- 앱: http://localhost:5173

### 프로덕션 빌드

#### 백엔드
```bash
cd server
npm install
npm start
```

#### 프론트엔드
```bash
cd ui
npm install
npm run build
```
- 빌드 결과물: `ui/dist/`

---

## 📦 주요 기술 스택

### 프론트엔드
- **React 19** - UI 라이브러리
- **Vite** - 빌드 도구
- **Vanilla CSS** - 스타일링

### 백엔드
- **Node.js** - 런타임
- **Express 5** - 웹 프레임워크
- **SQLite** - 개발 데이터베이스
- **PostgreSQL** - 배포 데이터베이스

---

## 🌐 배포

프로덕션 배포는 **Render.com**을 사용합니다.
자세한 내용은 [DEPLOYMENT.md](../DEPLOYMENT.md)를 참고하세요.

- **프론트엔드**: Static Site로 배포
- **백엔드**: Web Service로 배포
- **데이터베이스**: Render PostgreSQL 사용

---

## 📝 참고 문서

- [PRD.md](./PRD.md) - 제품 요구사항 문서
- [DEPLOYMENT.md](../DEPLOYMENT.md) - 배포 가이드
- [server/README.md](../server/README.md) - 백엔드 상세 문서
- [ui/README.md](../ui/README.md) - 프론트엔드 상세 문서

---

## 🎯 주요 기능

### 사용자 화면 (주문하기)
- ✅ 메뉴 조회 및 선택
- ✅ 옵션 선택 (샷 추가, 시럽 추가)
- ✅ 장바구니 관리
- ✅ 주문 생성

### 관리자 화면
- ✅ 주문 현황 통계
- ✅ 주문 상태 관리
- ✅ 재고 관리
- ✅ 실시간 주문 모니터링

---

*마지막 업데이트: 2025년 10월*

