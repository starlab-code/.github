# Starlab Agits

<div align="center">

![Commits](https://img.shields.io/badge/commits-475-79C83D?style=flat-square)
![Contributors](https://img.shields.io/badge/contributors-4-555555?style=flat-square)
![License](https://img.shields.io/badge/license-private-lightgrey?style=flat-square)

</div>

# Starlab Agits — 코딩 학습 · 자동 채점 플랫폼
> **학원 / 교실 환경을 위한 파이썬 문제 풀이 및 과제 운영 플랫폼** <br/> **V1 개발기간: 2026.04.20 ~ 2026.07.25** <br/> **V2 개발기간: 2026.07.28 ~**

## 버전 이력

| 버전 | 개발기간 | 상태 | 내용 |
| :---: | :---: | :---: | --- |
| **V1** | 2026.04.20 ~ 2026.07.25 | ✅ 개발 완료 | 문제 · 과제 · 제출 · 채점 · 계정 관리 전 기능, 웹 + Windows 데스크톱 앱, Render / Supabase 배포 |
| **V2** | 2026.07.28 ~ | 🔜 개발 중 | — |

## 배포 주소

**운영 중**

> **백엔드 서버** : Render Web Service (`render.yaml` 기준 배포) <br>
> **데이터베이스** : Supabase PostgreSQL (Seoul, `aws-1` pooler) <br>
> **데스크톱 앱** : `Starlab Code Setup <version>.exe` (Windows NSIS 설치 파일) <br>

<!-- > **개발 서버** : http://127.0.0.1:8000 <br>
> **프론트 서버** : http://localhost:5173 <br> -->

## 개발팀 소개

|      김태완       |          김경민         |       남도훈         |       박지연         |
| :------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   <img width="160px" src="https://avatars.githubusercontent.com/u/72859111?v=4"/>    |                      <img width="160px" src="https://github.com/rudals2755.png" />    |                   <img width="160px" src="https://avatars.githubusercontent.com/u/46241075?v=4"/>   |                   <img width="160px" src="https://avatars.githubusercontent.com/u/101178403?v=4"/>   |
|   [@TaewanKIM20](https://github.com/TaewanKIM20)   |    [@rudals2755](https://github.com/rudals2755)  | [@hoon3697](https://github.com/hoon3697)  | [@Hyrge](https://github.com/Hyrge)  |
| 프로젝트 리드 / 인프라 · 시스템 | 데이터베이스 / 품질 · 성능 | 프론트엔드 UI/UX 리드 | 풀스택 (문제 · 계정 도메인) |
| 2026.04.20 ~ 07.25 | 2026.04.29 ~ 07.23 | 2026.04.29 ~ 07.25 | 2026.04.29 ~ 07.24 |

### 담당 파트 (커밋 내역 기준)

> 아래 역할과 담당 파트는 **V1 기간(2026.04.20 ~ 2026.07.25)의 git 커밋 내역(작성 파일 · 커밋 메시지)을 기준으로** 정리했습니다.

#### 🔧 김태완 [@TaewanKIM20](https://github.com/TaewanKIM20) — 프로젝트 리드 / 인프라 · 시스템

2026.04.20 최초 커밋. 백엔드 뼈대와 채점 엔진을 세우고, 이후 채점을 브라우저 샌드박스로 이관한 시스템 파트 담당.

- **백엔드 초기 설계** — `judge.py`(서버 채점 엔진) · `models.py` · `db.py` · `auth.py` · `config.py` · `seed.py` · `main.py` 최초 작성. 이후 리팩토링의 기반이 된 데이터 모델과 채점 규약 수립
- **브라우저 샌드박스 채점 엔진** — 코드 실행을 학생 브라우저로 이관해 서버 실행 부담 제거. Python은 Pyodide, C는 clang(wasm) 컴파일 워커 + 자체 WASI 실행 워커로 구동하며, 서버와 출력 정규화를 일치시키고 숨김 테스트는 해시 비교로 정답 비노출 채점
- **COS 자격증 서브시스템** — 약 10,700줄 규모의 독립 모듈 (개발 진행 중)
- **스키마 마이그레이션** — 프론트엔드 데이터 계층을 신규 백엔드 계약(grouped assignment 모델)으로 전면 이관, `types.ts` 재작성
- **API 게이트웨이 재구축** — `frontend/src/app/api.ts` 요청 계층 재설계
- **인프라 · 배포** — DB 커넥션 풀 사이즈 / 세션 오류 대응, Render · Cloudflare Pages 배포 구성, 환경변수 및 CORS 관리, `README.md` · `DEPLOY_FREE.md` 작성


#### ⚙️ 김경민 [@rudals2755](https://github.com/rudals2755) — 데이터베이스 / 품질 · 성능

백엔드 도메인 로직 · 테스트 · CI 담당. **버그 수정에 회귀 테스트를 함께 추가**하는 패턴이 일관되게 나타남.

- **데이터 모델 · API 스키마 리팩토링** 및 스키마 패리티 DDL 직접 대조 검증
- **성능 개선** — 리더보드 전체 제출 메모리 집계 제거, 스트리밍 채점 폴링을 인프로세스 이벤트 기반으로 전환, `get_current_user` 중복 DB 세션 제거, pool status 로깅 미들웨어 조건화
- **보안 · 정합성** — 문제 / 카테고리 조회 API 인증 추가, 권한 검사 및 유효성 검증, HTTP 에러 상태 코드 표준화
- **참조 무결성** — 제출 · 과제 이력이 있는 학생 / 교사 / 문제 삭제 시 500 오류 수정
- `SubmissionJob` 보존 정책 및 정리 워커 추가
- **CI 구축** — PR / push마다 백엔드 pytest + 프론트 빌드를 실행하는 GitHub Actions
- 코드 에디터 개선 — 괄호 자동완성, 커서 이동 시 자동완성 처리, 라이트모드 탭 닫기 버튼

#### 🎨 남도훈 [@hoon3697](https://github.com/hoon3697) — 프론트엔드 UI/UX 리드

화면 설계 전반 담당.

- **화면 재설계** — 역할별 대시보드 재구성, 과제 관리 워크스페이스 개편, 계정 관리 화면 재구성
- **디자인 시스템** — 디자인 토큰 · 프리미티브 정리, 브랜드 및 상태 피드백 통일
- **반응형 대응** — 저해상도 개선, 테이블 가용 높이에 맞춘 페이지 행 수 자동 조정, 세로 잘림 방지
- **테이블 / 목록 UX** — 문제 · 제출 목록 테이블 통일, 페이지네이션 UI, 스크롤 동작 통일
- **접근성** — IDE · 모달 키보드 포커스 흐름 개선
- 화면 문구 · 아이콘 등 카피라이팅 및 정보 위계 정리, 프론트엔드 문서화(`ARCHITECTURE.md`)

#### 🧩 박지연 [@Hyrge](https://github.com/Hyrge) — 풀스택 (문제 · 계정 도메인)

프론트와 백엔드를 오가며 **문제 카테고리**와 **계정 관리** 두 기능을 세로로 관통해 구현.

- **계층형 문제 카테고리** — `CategorySelectionModal` 구현, 카테고리별 스타일 테마 정의, 해시태그 스타일 태그 UI, 태그 클릭 시 해당 태그 문제 검색
- 카테고리 필터링 API 연동 및 쿼리 버그 수정, 카테고리 CSS 모듈화 리팩토링
- **계정 관리** — 아이디 중복 확인, 비밀번호 확인 로직, 한글 / 대문자 정규식 검증, 반 이름 정규식 검사, 계정 삭제 제약 정리
- `AccountsView` 뷰 분리 및 폼 입력 UX 개선
- 공부 시간 측정 — 새로고침 후에도 유지, 선생님 계정은 '접속 시간'으로 표기
- 마크다운 백틱 강조로 문제 설명 가독성 개선, 카테고리 중첩 반영 테스트 보강

## 프로젝트 소개

Starlab Agits는 오프라인 코딩 수업을 그대로 옮겨온 형태의 학습 플랫폼입니다. 선생님이 문제를 등록하고 반 단위로 과제를 배정하면, 학생은 웹 또는 전용 데스크톱 앱에서 코드를 작성하고 제출합니다. 서버는 제출된 코드를 격리된 프로세스에서 실행해 테스트케이스 기준으로 자동 채점하고, 결과를 실시간 스트리밍으로 돌려줍니다.

기존 학원 운영에서 문제 배포 · 제출 수합 · 채점 · 진도 관리가 모두 수작업으로 흩어져 있던 것을 하나의 흐름으로 묶는 것이 목표입니다.

#### Starlab Agits turns a classroom into a coding lab.
Teachers register problems with test cases, assign them per classroom, and watch each student's progress in real time. Students write, run, and submit code — the server grades it automatically in an isolated sandbox.

#### Starlab Agits supports the following components.
1. Role-based dashboards for admin / teacher / student.
2. Automatic grading with streaming results and public test-case runs.
3. Hierarchical problem categories with tag filtering.
4. A locked-down desktop mode for exams (fullscreen, keyboard lock, exit password).

## 시작 가이드
### Requirements
For building and running the application you need:

- [Python 3.12](https://www.python.org/downloads/release/python-3120/)
- [Node.js 20](https://nodejs.org/en/blog/release/v20.11.0)
- [npm 10](https://www.npmjs.com/package/npm/v/10.2.4)
- Windows (데스크톱 앱 빌드 · 실행 시)

### Installation
``` bash
$ git clone https://github.com/starlab-code/starlab-code.git
$ cd starlab-code
```
#### Backend
```
$ cd backend
$ python -m venv .venv
$ .\.venv\Scripts\Activate.ps1
$ python -m pip install -r requirements.txt
$ python -m uvicorn app.main:app --reload
```
> 기본 로컬 DB는 `backend/starlab_code_mvp.db` SQLite 파일이며, 서버 시작 시 테이블 생성과 기본 문제 시드가 자동 실행됩니다.
> 확인: `http://127.0.0.1:8000/health` · `http://127.0.0.1:8000/docs`

#### Frontend
```
$ cd frontend
$ npm install
$ npm run dev
```
> 프론트엔드는 기본적으로 `http://127.0.0.1:8000` API를 호출합니다. 다른 백엔드를 바라봐야 하면 `frontend/.env`에 `VITE_API_BASE_URL`을 설정하세요.

#### Desktop
```
$ cd desktop
$ npm install
$ npm run dev
```
> 개발 모드 데스크톱 앱은 `http://localhost:5173`을 엽니다. 백엔드와 프론트엔드가 먼저 실행되어 있어야 합니다.
> Windows 설치 파일 생성: 루트에서 `npm run dist`

---

## Stacks 🐈

### Environment
![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-007ACC?style=for-the-badge&logo=Visual%20Studio%20Code&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=Git&logoColor=white)
![Github](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=GitHub&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=GitHub%20Actions&logoColor=white)

### Config
![npm](https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=Vite&logoColor=white)

### Development
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=FastAPI&logoColor=white)
![SQLModel](https://img.shields.io/badge/SQLModel-7E56C2?style=for-the-badge&logo=SQLAlchemy&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=TypeScript&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Electron](https://img.shields.io/badge/Electron-47848F?style=for-the-badge&logo=Electron&logoColor=white)
![Blockly](https://img.shields.io/badge/Blockly-4285F4?style=for-the-badge&logo=Google&logoColor=white)

### Database & Deploy
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=PostgreSQL&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=Supabase&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=SQLite&logoColor=white)
![Render](https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=Render&logoColor=white)

### Test
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=Pytest&logoColor=white)

---
## 화면 구성 📺
| 로그인 페이지  |  대시보드 (선생님)   |
| :-------------------------------------------: | :------------: |
|  <img width="329" src="../docs/screenshots/login.png"/> |  <img width="329" src="../docs/screenshots/teacher-home.png"/>|
| 문제 목록 페이지   |  풀이 · 채점 페이지   |
| <img width="329" src="../docs/screenshots/problem-list.png"/>   |  <img width="329" src="../docs/screenshots/solve.png"/>     |

---
## V1 주요 기능

### ⭐️ 역할 기반 화면 분기
- 관리자 / 선생님 / 학생 각각 다른 대시보드 · 사이드바 · 권한
- JWT 인증, 세션은 localStorage로 유지

### ⭐️ 브라우저 샌드박스 자동 채점
- **채점은 학생 브라우저에서 실행되고 서버는 결과만 기록** — 앱 서버의 코드 실행 부담 0
- Python은 Pyodide, C는 clang(wasm) 컴파일 워커 + 자체 WASI 실행 워커로 구동
- 숨김 테스트케이스는 정답 평문 대신 `expected_sha256`만 내려보내 정답 역산 없이 판정
- 출력 정규화 규약을 서버 `judge.py`와 바이트 단위로 일치시켜 판정 불일치(verdict drift) 방지
- 제출 전 공개 테스트케이스로 직접 실행 가능

### ⭐️ 서버 채점 폴백
- 서버측 채점(`SubmissionJob` 큐 + 워커 스레드 subprocess 실행)은 **평시 사용하지 않는 폴백 경로**
- 격리 헤더 미지원 · CSP 차단 등으로 브라우저 채점이 불가능할 때만 동작
- 폴백 시에는 인프로세스 이벤트 기반 스트리밍으로 채점 결과 실시간 전달

### ⭐️ 과제 배정 및 진행 현황 관리
- 문제를 선택해 반 단위로 과제 배정, 반별 토글 UI
- 학생별 진행 현황 그리드, 전체 누적 랭킹 집계

### ⭐️ 계층형 문제 카테고리 및 태그 검색
- 카테고리 선택 모달을 통한 계층형 필터링
- 해시태그 스타일 태그 클릭 시 해당 태그 문제 즉시 검색

### ⭐️ COS 자격증 탭
- Blockly 기반 스크래치 워크스페이스와 LEGO SPIKE 시뮬레이터를 브라우저에서 직접 구동
- 자격증 문제 풀이 · 자동 채점 제공, 역할에 따라 탭 노출 제어

---
## 아키텍쳐

### 디렉토리 구조
```bash
├── README.md
├── package.json                    : npm workspaces 및 루트 스크립트
├── render.yaml                     : Render 백엔드 배포 설정
├── .github/workflows/ci.yml        : PR·push마다 pytest + 프론트 빌드
├── backend : FastAPI API 서버
│   ├── app
│   │   ├── main.py                 : 앱 초기화 및 라우터 등록
│   │   ├── auth.py                 : JWT 인증 / 비밀번호 처리
│   │   ├── config.py               : 환경변수 설정
│   │   ├── db.py                   : DB 엔진 / 세션
│   │   ├── judge.py                : 제출 코드 실행 및 채점 엔진
│   │   ├── models.py               : SQLModel 데이터 모델 / 응답 타입
│   │   ├── seed.py                 : 기본 문제 · 계정 시드
│   │   ├── api : HTTP 라우터 계층
│   │   │   ├── auth.py             : 인증 엔드포인트
│   │   │   ├── assignments.py      : 과제 엔드포인트
│   │   │   ├── classrooms.py       : 클래스룸 엔드포인트
│   │   │   ├── dashboard.py        : 대시보드 엔드포인트
│   │   │   ├── problem.py          : 문제 / 테스트케이스 엔드포인트
│   │   │   ├── submissions.py      : 제출 / 채점 엔드포인트
│   │   │   └── users.py            : 사용자 엔드포인트
│   │   ├── services : DB 쿼리 · 트랜잭션 계층
│   │   └── utils : 순수 헬퍼 함수
│   ├── schema                      : 타겟 스키마 DDL
│   ├── tests                       : pytest 스위트
│   └── requirements.txt
├── frontend : React + Vite 웹 앱
│   ├── src
│   │   ├── main.tsx                : React 앱 진입점
│   │   ├── App.tsx                 : 인증 · 서버 데이터 · 화면 전환 조정
│   │   ├── config.ts               : API URL, 앱 버전
│   │   ├── types.ts                : 프론트엔드 공통 타입
│   │   ├── app : 화면이 아닌 앱 일반 로직
│   │   │   ├── api.ts              : fetch 래퍼 및 API 오류 타입
│   │   │   ├── editor.ts           : 언어별 기본 코드와 draft key
│   │   │   ├── forms.ts            : 문제 / 과제 / 계정 폼 초기값
│   │   │   └── session.ts          : 로그인 세션 localStorage 관리
│   │   ├── components : 재사용 UI 컴포넌트
│   │   │   ├── AppChrome.tsx       : 헤더, 사이드바, 토스트, 푸터
│   │   │   ├── CodeEditor.tsx      : 풀이 화면 코드 에디터
│   │   │   ├── Badges.tsx          : 난이도 / 채점 상태 배지
│   │   │   └── Modals.tsx          : 확인 / 학생 이동 / 비밀번호 변경 모달
│   │   ├── hooks : 화면에서 분리한 상태 로직
│   │   ├── views : 역할별 화면 컴포넌트
│   │   │   ├── AuthViews.tsx       : 로그인 화면
│   │   │   ├── DashboardViews.tsx  : 역할별 대시보드
│   │   │   ├── AccountsView.tsx    : 계정 관리
│   │   │   ├── SolveView.tsx       : 풀이 · 채점 화면
│   │   │   ├── assignments         : 과제 관리 화면
│   │   │   └── problems            : 문제 목록 / 카테고리 모달
│   │   └── styles : 토큰 → 레이아웃 → 화면별 → 반응형 순
│   ├── public
│   └── package.json
└── desktop : Electron Windows 앱
    ├── src
    │   ├── main.cjs                : Electron 메인 프로세스
    │   ├── preload.cjs             : Renderer IPC 브리지
    │   ├── kiosk-hook.cjs          : 학생 모드 잠금 훅
    │   ├── update.html             : 업데이트 화면
    │   └── exit-prompt.html        : 학생 모드 종료 비밀번호 화면
    ├── scripts
    │   └── build-frontend.cjs      : 프론트 빌드 후 desktop/app으로 복사
    ├── assets
    └── package.json
```
