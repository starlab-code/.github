# Starlab AGIT

<div align="center">

![Commits](https://img.shields.io/badge/commits-730-79C83D?style=flat-square)
![Contributors](https://img.shields.io/badge/contributors-6-555555?style=flat-square)
![Version](https://img.shields.io/badge/version-V2-6C5CE7?style=flat-square)
![Infra](https://img.shields.io/badge/infra-AWS%20Lambda-FF9900?style=flat-square)
![License](https://img.shields.io/badge/license-private-lightgrey?style=flat-square)

</div>

# AGIT — 코딩 · 피지컬 AI 학습 플랫폼

> **스타랩 수원의 수업 · 과제 · 채점 · 학습 리포트를 하나로 운영하는 학원용 학습 플랫폼** <br/>
> **V1 개발기간: 2026.04.20 ~ 2026.07.25** <br/>
> **V2 개발기간: 2026.07.28 ~ 현재 (2026.11.25 기준 운영 중)** <br/>
> **서비스 주소: https://agits.co.kr**

## 목차

1. [버전 이력](#버전-이력)
2. [개발팀과 기여도](#개발팀과-기여도)
3. [프로젝트 소개](#프로젝트-소개)
4. [화면 구성 (V2)](#화면-구성-v2)
5. [V2 주요 기능](#v2-주요-기능)
6. [인프라: Render → ECS → Lambda](#인프라-render--ecs--lambda)
7. [아키텍처와 디렉토리 구조](#아키텍처와-디렉토리-구조)
8. [시작 가이드](#시작-가이드)
9. [Stacks](#stacks-)

---

## 버전 이력

| 버전 | 개발기간 | 상태 | 내용 |
| :---: | :---: | :---: | --- |
| **V1** | 2026.04.20 ~ 2026.07.25 | ✅ 개발 완료 | 문제 · 과제 · 제출 · 채점 · 계정 관리, 웹 + Windows 데스크톱 앱, Render / Supabase 배포 |
| **V2** | 2026.07.28 ~ | 🟢 운영 중 | 강의실(교안 · 커리큘럼), 아두이노 · COS 자격증, AI 학습 도우미 · AI 보고서 · AI 의심 신호, 공개 소개 페이지, **AWS Lambda 서버리스 운영** |

**V2에서 바뀐 것 한눈에 보기**

| 구분 | V1 | V2 |
| --- | --- | --- |
| 서비스 | 문제 풀이 · 과제 플랫폼 | 학원 전체 수업 플랫폼 (공개 소개 페이지 + 강의실 + 자격증 + 문제 + 과제) |
| 학습 콘텐츠 | 문제 단위 | **강의실 과정 12개** (Python · C · 자료구조 · 아두이노 · AI · YOLO · 자율주행 등), 차시 · 교안 · 예제 · 미션 |
| 채점 | 브라우저 채점 + 서버 채점 폴백 | **브라우저 채점으로 일원화** (Python · C · 아두이노 AVR 모두 브라우저 WebAssembly) |
| AI | 없음 | AI 학습 도우미, AI 학습 보고서, AI 사용 의심 신호, 선생님용 AI 질문 기록 |
| 배포 | Render + Supabase | AWS ECS Fargate (2026.09) → **AWS Lambda + CloudFront/S3 (2026.11)** |
| 클라이언트 | 웹 + Electron 데스크톱 | **웹 단독** (Electron 셸은 코드만 남고 사용하지 않음) |
| 규모 | — | API 라우트 119개 · DB 테이블 43개 · 테스트 백엔드 455개 + 프런트 테스트 파일 77개 |

---

## 개발팀과 기여도

### 개발팀 소개

|      김태완       |          김경민         |       남도훈         |       박지연         |
| :---: | :---: | :---: | :---: |
| <img width="140px" src="https://avatars.githubusercontent.com/u/72859111?v=4"/> | <img width="140px" src="https://github.com/rudals2755.png" /> | <img width="140px" src="https://avatars.githubusercontent.com/u/46241075?v=4"/> | <img width="140px" src="https://avatars.githubusercontent.com/u/101178403?v=4"/> |
| [@TaewanKIM20](https://github.com/TaewanKIM20) | [@rudals2755](https://github.com/rudals2755) · [@kyoungmin24](https://github.com/kyoungmin24) | [@hoon3697](https://github.com/hoon3697) | [@Hyrge](https://github.com/Hyrge) |
| 프로젝트 리드 / 인프라 · AI · 학습 콘텐츠 | 강의실 · 과제 도메인 / 품질 · 테스트 | 프론트엔드 UI/UX 리드 | 풀스택 (문제 · 계정 도메인) |
| V1 · V2 (2026.04.20 ~) | V1 · V2 (2026.04.29 ~) | V1 (2026.04.29 ~ 07.25) | V1 (2026.04.29 ~ 07.24) |

| haju0423 | ajidaeng | chaeewone | choala |
| :---: | :---: | :---: | :---: |
| <img width="100px" src="https://github.com/haju0423.png" /> | <img width="100px" src="https://github.com/ajidaeng.png" /> | <img width="100px" src="https://github.com/chaeewone.png" /> | <img width="100px" src="https://github.com/choala.png" /> |
| [@haju0423](https://github.com/haju0423) | [@ajidaeng](https://github.com/ajidaeng) | [@chaeewone](https://github.com/chaeewone) | [@choala](https://github.com/choala) |
| 백엔드 · CI 유지보수 | 교안 변환 워커 유지보수 | V2 합류 | V2 합류 · 소개 페이지 |
| V2 (2026.11 ~) | V2 (2026.11 ~) | V2 (2026.11 ~) | V2 (2026.11 ~) |

### 📊 기여도 한눈에 보기

> **기준:** `starlab-code` 저장소 `dev` 브랜치, 2026.11.25.
> - **커밋** — merge 커밋 제외. V1은 2026.07.25까지, V2는 2026.07.28부터.
> - **남아있는 코드** — 지금 저장소에 남아 있는 줄을 `git blame -w`로 작성자별로 센 값. 직접 작성한 소스(`.py .ts .tsx .css .cjs .yml .sh` 등)만 셌고, 데이터 JSON · 벤더 바이너리 · 이미지 · 교안 원본 · 생성물은 뺐습니다.
> - **학습 콘텐츠** — 커리큘럼 · 자격증 문제 시드처럼 코드 형태로 들어간 콘텐츠 파일(`learning_seed*.py`, `seed.py`, `cospro/`)은 따로 셌습니다.
> - 같은 사람의 두 계정(`rudals2755` · `kyoungmin24`, `Kevin` · `hoon3697`)은 합쳤고, 봇 커밋은 뺐습니다.

| 이름 | 커밋 V1 | 커밋 V2 | 커밋 합계 | 남아있는 코드 | 비중 | 학습 콘텐츠 |
| --- | ---: | ---: | ---: | ---: | :--- | ---: |
| **김태완** | 75 | 110 | **185** | **87,298줄** | `████████████▋` 63.3% | 20,802줄 |
| **김경민** | 67 | 82 | **149** | **24,877줄** | `███▌` 18.0% | 2,419줄 |
| **남도훈** | 185 | — | **185** | **20,294줄** | `██▉` 14.7% | — |
| **박지연** | 83 | — | **83** | **5,331줄** | `▊` 3.9% | 39줄 |
| haju0423 | — | 2 | 2 | 21줄 | 0.02% | — |
| ajidaeng | — | 1 | 1 | 22줄 | 0.02% | — |
| **합계** | 410 | 195 | **605** | **137,935줄** | | 23,260줄 |

<sub>chaeewone · choala는 2026.11 합류로 아직 코드 커밋이 없습니다. "남아있는 코드"는 나중에 다른 사람이 고친 줄은 마지막 작성자에게 넘어가므로, 초기 설계나 이미 지워진 코드의 기여는 커밋 수로 함께 보세요.</sub>

### 🗺️ 영역별 주 작성자 (현재 코드 기준 줄 수)

| 영역 | 경로 | 김태완 | 김경민 | 남도훈 | 박지연 |
| --- | --- | ---: | ---: | ---: | ---: |
| **인프라 · 배포** | `infra/` `scripts/` `.github/workflows/` | 2,606 | 48 | | |
| **AI 학습 도우미** | `assistant/` `frontend/src/components/assistant` | 2,673 | | | |
| **AI 보고서** | `api/reports*` `report_worker.py` `views/reports` | 1,207 | 2 | | |
| **AI 의심 신호** | `backend/app/signals` `signals/` | 2,046 | | | |
| **교안 변환 워커** | `converter/` | 277 | | | |
| **강의실 (백엔드)** | `api/learning.py` `learning_decks.py` | 1,220 | 710 | | |
| **강의실 (화면)** | `frontend/src/views/classroom` | 4,093 | 3,149 | | |
| **아두이노** | `frontend/src/arduino` | 7,243 | 295 | | |
| **COS 자격증** | `frontend/src/cert` `api/cos.py` | 12,102 | 3 | | |
| **브라우저 채점 엔진** | `frontend/src/judge` | 3,097 | 230 | 84 | |
| **공개 소개 페이지** | `frontend/src/views/public` | 4,583 | 326 | | |
| **문제 대량 등록 (엑셀)** | `api/problem_drafts.py` | 82 | 485 | | |
| **과제 (백엔드)** | `api/assignments.py` `services/assignments.py` | 10 | 896 | | 75 |
| **과제 (화면)** | `frontend/src/views/assignments` | 348 | 317 | 1,414 | |
| **문제 화면** | `frontend/src/views/problems` | | 2,068 | 2,409 | 1,981 |
| **계정 관리** | `views/AccountsView.tsx` | | 111 | 582 | 264 |
| **풀이 화면** | `views/SolveView.tsx` | 70 | 126 | 573 | |
| **대시보드 API** | `api/dashboard.py` | 359 | 212 | | 126 |
| **공통 컴포넌트 · 훅** | `frontend/src/components` `hooks` | 3,560 | 954 | 4,388 | 532 |
| **스타일 · 디자인 시스템** | `frontend/src/styles` | 13,761 | 5,020 | 6,704 | |
| **백엔드 테스트** | `backend/tests` | 4,763 | 3,466 | | 740 |

---

### 담당 파트

> V1 내용은 V1 기간 커밋 내역 기준으로 정리했던 내용을 그대로 두었고, V2 내용은 2026.07.28 이후 커밋과 지금 남아 있는 코드를 기준으로 새로 정리했습니다.

#### 🔧 김태완 [@TaewanKIM20](https://github.com/TaewanKIM20) — 프로젝트 리드 / 인프라 · AI · 학습 콘텐츠

2026.04.20 최초 커밋. 백엔드 뼈대와 채점 엔진을 세웠고, V2에서는 운영 인프라 전체(ECS → Lambda 전환)와 AI 기능, 아두이노 · 자격증 · 강의실 콘텐츠를 담당.

**V2**
- **AWS 운영 인프라 설계 · 전환** — ECS Express Mode 배포 구성(2026.09.19), 이어서 **Lambda + CloudFront/S3 서버리스 전환**(2026.11.04 컷오버, 11.10 ECS 삭제). SAM 템플릿(`infra/lambda/`), 배포 · 마이그레이션 · 부하 시험 스크립트(`scripts/`), 바뀐 영역만 배포하는 CI/CD와 브랜치 보호 워크플로 14종
- **운영 장애 대응** — 수업 시작 몰림 때 DB 연결 한도 초과(5xx)를 NullPool + 흩뜨린 재시도 + 503/Retry-After로 해결, 탭별 동시 API 요청을 3개로 제한, SnapStart 옛 버전 정리로 보관료 누적 차단
- **브라우저 채점 일원화** — 서버 채점 경로를 제거하고(2026.08.03) Python · C 채점을 브라우저로 통일 (`frontend/src/judge`)
- **AI 학습 도우미** — 별도 Lambda(`assistant/`), Bedrock 스트리밍 응답, DynamoDB 사용량 한도 · 질문 기록, 정답 코드 노출 차단과 모델 기반 정답 판정(Qwen3-32B), 선생님용 AI 질문 기록 화면
- **AI 학습 보고서** — 학생별 학습 근거를 모아 Bedrock으로 보고서 생성, HTTP 30초 제한을 피하려고 DynamoDB 작업 + Streams + worker Lambda로 비동기화, PDF 인쇄
- **AI 사용 의심 신호** — 제출 코드의 AI 사용 의심도를 제출 시점에 1~3ms로 계산하는 엔진(`backend/app/signals`)과 해답 뱅크 · 또래 분포를 만드는 오프라인 파이프라인(`signals/`)
- **아두이노** — 가상 보드 시뮬레이션, 회로도, 시리얼 모니터, 실제 보드 연결(Web Serial), 아두이노 기초 · 응용 커리큘럼
- **COS · COS PRO 자격증** — Blockly 기반 블록코딩 실기 환경과 회차별 모의고사, COS PRO 문제 은행(`backend/app/cospro`)
- **강의실 교안** — 차시 교안(PPT · PDF) 업로드와 페이지 선택, 교안 변환 Lambda(LibreOffice + PyMuPDF), 커리큘럼 편집, 학습 작업 공간 · 집중 감시
- **공개 소개 페이지** — 학원 소개 · 과정 · 로드맵 · 수상 기록 · 공개 문제 라이브러리

<details>
<summary><b>V1</b></summary>

- **백엔드 초기 설계** — `judge.py`(서버 채점 엔진) · `models.py` · `db.py` · `auth.py` · `config.py` · `seed.py` · `main.py` 최초 작성. 이후 리팩토링의 기반이 된 데이터 모델과 채점 규약 수립
- **브라우저 샌드박스 채점 엔진** — 코드 실행을 학생 브라우저로 이관해 서버 실행 부담 제거. Python은 Pyodide, C는 clang(wasm) 컴파일 워커 + 자체 WASI 실행 워커로 구동하며, 서버와 출력 정규화를 일치시키고 숨김 테스트는 해시 비교로 정답 비노출 채점
- **COS 자격증 서브시스템** — 약 10,700줄 규모의 독립 모듈
- **스키마 마이그레이션** — 프론트엔드 데이터 계층을 신규 백엔드 계약(grouped assignment 모델)으로 전면 이관, `types.ts` 재작성
- **API 게이트웨이 재구축** — `frontend/src/app/api.ts` 요청 계층 재설계
- **인프라 · 배포** — DB 커넥션 풀 사이즈 / 세션 오류 대응, Render · Cloudflare Pages 배포 구성, 환경변수 및 CORS 관리, `README.md` · `DEPLOY_FREE.md` 작성

</details>

#### ⚙️ 김경민 [@rudals2755](https://github.com/rudals2755) · [@kyoungmin24](https://github.com/kyoungmin24) — 강의실 · 과제 도메인 / 품질 · 테스트

V1에서는 백엔드 도메인 로직 · 테스트 · CI, V2에서는 **강의실 학습 흐름의 첫 설계**와 과제 · 문제 등록 도메인을 담당. 버그 수정에 회귀 테스트를 함께 추가하는 패턴이 V2에서도 이어짐(현재 백엔드 테스트 3,466줄).

**V2**
- **강의실 학습 흐름** — 강의실 탭 프로토타입(2026.08.17)과 과정별 강의실 진입, 코드 에디터 실행/채점 분리, 노트북 · 실습 데이터 기능, 커리큘럼별 학생 학습 현황
- **커리큘럼 콘텐츠** — Python 기초(실제 수업 흐름 기준 재작성) · C언어 기초 · 자료구조&알고리즘 커리큘럼, 차시별 추천 문제
- **아두이노 브라우저 컴파일** — 서버 컴파일러 대신 avr-gcc WebAssembly로 브라우저에서 HEX를 만드는 방식으로 변경(2026.11.08), 아두이노 에디터 자동 완성 · 문법 하이라이트
- **문제 스테이징 등록** — 엑셀 템플릿 업로드 → 검증 → 수정 → 등록하는 초안 흐름(`api/problem_drafts.py`), 문제 관리의 C언어 지원
- **과제** — 학생 선택 배정, 과제 관리 탭 무한 스크롤 · 서버 측 검색/필터/정렬(`services/assignments.py`)
- **화면 · UX** — Growlytics 기반 디자인 시스템 적용, 로그인 화면 개편, 화면 오류 복구 경계, 학생 관리 화면 개선, 반 담당 선생님 변경, 학생 홈 추천 문제, 역할별 사용 가이드, 소개 페이지 애니메이션
- **코드 품질** — `datetime.utcnow()`를 프로젝트 함수 `utc_now()`로 교체(Python 3.12 deprecation 대응)

<details>
<summary><b>V1</b></summary>

- **데이터 모델 · API 스키마 리팩토링** 및 스키마 패리티 DDL 직접 대조 검증
- **성능 개선** — 리더보드 전체 제출 메모리 집계 제거, 스트리밍 채점 폴링을 인프로세스 이벤트 기반으로 전환, `get_current_user` 중복 DB 세션 제거, pool status 로깅 미들웨어 조건화
- **보안 · 정합성** — 문제 / 카테고리 조회 API 인증 추가, 권한 검사 및 유효성 검증, HTTP 에러 상태 코드 표준화
- **참조 무결성** — 제출 · 과제 이력이 있는 학생 / 교사 / 문제 삭제 시 500 오류 수정
- `SubmissionJob` 보존 정책 및 정리 워커 추가
- **CI 구축** — PR / push마다 백엔드 pytest + 프론트 빌드를 실행하는 GitHub Actions
- 코드 에디터 개선 — 괄호 자동완성, 커서 이동 시 자동완성 처리, 라이트모드 탭 닫기 버튼

</details>

#### 🎨 남도훈 [@hoon3697](https://github.com/hoon3697) — 프론트엔드 UI/UX 리드 (V1)

V1 화면 설계 전반 담당. V1 커밋 185개로 V1 최다 커밋. 지금도 과제 화면 · 문제 화면 · 계정 관리 · 풀이 화면 · 공통 훅의 상당 부분이 남아 있음(현재 코드 20,294줄).

- **화면 재설계** — 역할별 대시보드 재구성, 과제 관리 워크스페이스 개편, 계정 관리 화면 재구성
- **디자인 시스템** — 디자인 토큰 · 프리미티브 정리, 브랜드 및 상태 피드백 통일
- **반응형 대응** — 저해상도 개선, 테이블 가용 높이에 맞춘 페이지 행 수 자동 조정, 세로 잘림 방지
- **테이블 / 목록 UX** — 문제 · 제출 목록 테이블 통일, 페이지네이션 UI, 스크롤 동작 통일
- **접근성** — IDE · 모달 키보드 포커스 흐름 개선
- 화면 문구 · 아이콘 등 카피라이팅 및 정보 위계 정리, 프론트엔드 문서화(`ARCHITECTURE.md`)

#### 🧩 박지연 [@Hyrge](https://github.com/Hyrge) — 풀스택 (문제 · 계정 도메인, V1)

프론트와 백엔드를 오가며 **문제 카테고리**와 **계정 관리** 두 기능을 세로로 관통해 구현. 지금도 문제 화면 1,981줄 · 백엔드 테스트 740줄이 남아 있음.

- **계층형 문제 카테고리** — `CategorySelectionModal` 구현, 카테고리별 스타일 테마 정의, 해시태그 스타일 태그 UI, 태그 클릭 시 해당 태그 문제 검색
- 카테고리 필터링 API 연동 및 쿼리 버그 수정, 카테고리 CSS 모듈화 리팩토링
- **계정 관리** — 아이디 중복 확인, 비밀번호 확인 로직, 한글 / 대문자 정규식 검증, 반 이름 정규식 검사, 계정 삭제 제약 정리
- `AccountsView` 뷰 분리 및 폼 입력 UX 개선
- 공부 시간 측정 — 새로고침 후에도 유지, 선생님 계정은 '접속 시간'으로 표기
- 마크다운 백틱 강조로 문제 설명 가독성 개선, 카테고리 중첩 반영 테스트 보강

#### 🛠️ V2 합류 멤버 (2026.11 ~)

| 멤버 | 기여 |
| --- | --- |
| [@haju0423](https://github.com/haju0423) | 백엔드 · AI 도우미 JWT 라이브러리를 `python-jose`에서 `PyJWT`로 교체 ([#142](https://github.com/starlab-code/starlab-code/pull/142)), 프런트 테스트 실패 2건 수정과 CI의 실패 무시 설정 제거 ([#140](https://github.com/starlab-code/starlab-code/pull/140)) |
| [@ajidaeng](https://github.com/ajidaeng) | 교안 변환 Lambda의 Pillow · PyMuPDF 보안 업데이트 ([#141](https://github.com/starlab-code/starlab-code/pull/141)) |
| [@choala](https://github.com/choala) | 소개 페이지 수업 사진 교체 이슈 ([#134](https://github.com/starlab-code/starlab-code/issues/134)) |
| [@chaeewone](https://github.com/chaeewone) | 2026.11 합류 |

---

## 프로젝트 소개

AGIT은 스타랩 수원의 오프라인 코딩 · 로봇 수업을 그대로 옮겨 온 학습 플랫폼입니다. 선생님은 강의실 과정과 교안으로 수업하고, 문제를 반 단위로 과제로 배정합니다. 학생은 웹에서 예제와 미션을 실행하고 제출합니다. 채점은 학생 브라우저 안에서 실행되고, 서버는 결과와 학습 기록만 저장합니다.

V1이 "문제 배포 · 제출 수합 · 채점 · 진도 관리를 하나로 묶는 것"이었다면, V2는 여기에 **수업 자체(강의실 · 교안 · 아두이노 · 자격증)와 AI 기반 학습 지도(도우미 · 보고서 · 의심 신호)**를 더하고, 운영 비용을 학원 규모에 맞게 낮추는 것이 목표였습니다.

#### AGIT turns a classroom into a coding lab.
Teachers run lessons from slide decks and curricula, assign problems per class, and track each student's progress. Students run examples and missions in the browser — Python, C and Arduino code is compiled and graded client-side with WebAssembly. An AI tutor gives hints without giving away answers, and teachers get AI-written learning reports.

#### AGIT supports the following components.
1. Public landing site and problem library for visitors.
2. Classroom courses with lessons, slide decks, examples, missions and notebooks.
3. In-browser grading for Python (Pyodide), C (clang wasm) and Arduino (avr-gcc wasm + virtual board).
4. COS block-coding certification practice and COS PRO question bank.
5. AI learning assistant, AI learning reports and AI-usage suspicion signals.
6. Serverless operation on AWS Lambda, CloudFront and S3.

---

## 화면 구성 (V2)

> 운영 사이트 https://agits.co.kr 를 2026.11.25에 캡처했습니다. 학생 · 선생님의 실명과 아이디는 캡처할 때 `학생A` · `student01` · `선생님A` 같은 가명으로 바꿨습니다.

### 공개 페이지 (로그인 전)

| 소개 페이지 | 공개 문제 라이브러리 |
| :---: | :---: |
| <img width="420" src="../docs/screenshots/v2/01-intro.png"/> | <img width="420" src="../docs/screenshots/v2/02-public-problems.png"/> |
| 학원 소개 · 과정 · 로드맵 · 수상 기록 · 상담 신청 | 로그인 없이 문제를 언어 · 분류 · 난이도로 탐색 |

### 반 현황 (선생님 홈)

<img width="860" src="../docs/screenshots/v2/03-teacher-home.png"/>

반 · 학생 · 기간을 고르면 최근 학습 성과, 6개 축 학습 역량, 전체 학생 랭킹, 연간 학습 기록, 과제별 진행을 한 화면에 보여 줍니다. 여기서 **AI 보고서 저장**을 누르면 학생별 AI 학습 보고서를 만들어 PDF로 인쇄합니다.

### 강의실

| 강의 목록 | 과정 대시보드 |
| :---: | :---: |
| <img width="420" src="../docs/screenshots/v2/04-classroom.png"/> | <img width="420" src="../docs/screenshots/v2/05-course-dashboard.png"/> |
| 단계별(E-S · E-T · E-A · E-R) 과정 12개, 반별 공개 토글 | 진도율 · 다음 학습 항목 · 차시별 커리큘럼, 커리큘럼 편집 |
| **학습 작업 공간** | **AI 학습 도우미** |
| <img width="420" src="../docs/screenshots/v2/07-lesson-workspace.png"/> | <img width="420" src="../docs/screenshots/v2/08-ai-assistant.png"/> |
| 왼쪽 설명 · 학습 포인트 · 교안, 오른쪽 코드 실행 · 채점 | 개념 · 로직 확인 · 오류 해석 · 사이트 사용법. 정답 코드는 주지 않고, 질문은 선생님이 볼 수 있음 |

| 과정별 학생 학습 현황 |
| :---: |
| <img width="860" src="../docs/screenshots/v2/06-course-students.png"/> |

### 아두이노

| 아두이노 과정 | 아두이노 작업 공간 |
| :---: | :---: |
| <img width="420" src="../docs/screenshots/v2/09-arduino-course.png"/> | <img width="420" src="../docs/screenshots/v2/10-arduino-workspace.png"/> |
| 교안 7개 기반 7차시 · 71개 항목 | 교안 페이지 · 회로도 · 가상 보드 · 실제 보드 연결 · 시리얼 모니터. 컴파일은 브라우저 안의 avr-gcc WebAssembly |

### 자격증 (COS · COS PRO)

| 자격증 목록 | COS 급수 과정 | 블록코딩 실기 |
| :---: | :---: | :---: |
| <img width="280" src="../docs/screenshots/v2/11-certification.png"/> | <img width="280" src="../docs/screenshots/v2/12-cos-course.png"/> | <img width="280" src="../docs/screenshots/v2/13-cos-block-coding.png"/> |
| COS 1~4급 · COS PRO | 회차별 모의고사, 응시율 · 점수 | Blockly 블록 · 무대 · 스프라이트, 제출하면 바로 채점 |

### 문제와 풀이

| 문제 라이브러리 | 문제 상세 | 풀이 · 채점 |
| :---: | :---: | :---: |
| <img width="280" src="../docs/screenshots/v2/14-problem-library.png"/> | <img width="280" src="../docs/screenshots/v2/15-problem-detail.png"/> | <img width="280" src="../docs/screenshots/v2/16-solve.png"/> |
| 212개 문제, 난이도 · 언어 · 분류 필터 | 풀이 전 확인 · 문제 설명 · 과제 배정 | Python 3 · C 전환, 실행 · 채점 · 제출, 공개 테스트 |

### 선생님 운영 화면

| 과제 관리 | 학생 제출 |
| :---: | :---: |
| <img width="420" src="../docs/screenshots/v2/17-assignments.png"/> | <img width="420" src="../docs/screenshots/v2/18-submissions.png"/> |
| 과제별 제출 · 정답 · 미제출 · 지각, 학생별 **AI 의심도** | 반 · 학생 · 문제 · 결과별 제출 기록과 코드 보기 |
| **AI 질문 기록** | **문제 관리 (스테이징 등록)** |
| <img width="420" src="../docs/screenshots/v2/19-ai-questions.png"/> | <img width="420" src="../docs/screenshots/v2/20-problem-staging.png"/> |
| 학생이 AI 도우미에 한 질문, 정답 요청 · 노출 차단 건수 | 엑셀 업로드 → 형식 검증 → 실제 테스트 채점 → 등록 |
| **학생 관리** | |
| <img width="420" src="../docs/screenshots/v2/21-accounts.png"/> | |
| 학생 · 선생님 계정, 반 · 담당 선생님 · 자격증 | |

<details>
<summary><b>V1 화면 구성</b></summary>

| 로그인 페이지  |  대시보드 (선생님)   |
| :-------------------------------------------: | :------------: |
|  <img width="329" src="../docs/screenshots/login.png"/> |  <img width="329" src="../docs/screenshots/teacher-home.png"/>|
| 문제 목록 페이지   |  풀이 · 채점 페이지   |
| <img width="329" src="../docs/screenshots/problem-list.png"/>   |  <img width="329" src="../docs/screenshots/solve.png"/>     |

</details>

---

## V2 주요 기능

### ⭐️ 강의실 — 수업을 그대로 옮긴 과정 · 차시 · 교안
- 과정 12개: Python 기초 · C언어 기초 · 자료구조&알고리즘 · 아두이노 기초/응용 · AI 기초 · AI 에이전트 · YOLO · 자동화 스크립트 · Turtle · 자율주행 · Manipulator
- 차시마다 예제 · 미션 · 문제, 실제 수업 교안(PPT · PDF)을 페이지 단위로 붙여 보기
- 교안 업로드 → **교안 변환 Lambda**(LibreOffice + PyMuPDF)가 페이지 이미지로 바꿔 S3에 SHA-256 이름으로 저장
- 노트북 · 실습 데이터, 반별 공개 토글, 커리큘럼 편집, 과정별 학생 학습 현황, 학습 작업 공간 집중 감시

### ⭐️ 브라우저 채점 일원화
- Python은 Pyodide, C는 clang(wasm) + 자체 WASI 실행 워커, 아두이노는 avr-gcc 7.3 WebAssembly로 모두 **학생 브라우저에서 실행**
- 서버는 결과만 검증 · 저장하므로 Lambda에서 사용자 코드를 실행하지 않음 (V1의 서버 채점 폴백은 2026.08.03 제거)
- 숨김 테스트케이스는 정답 평문 대신 `expected_sha256`만 내려보내 정답 역산 없이 판정
- C 채점에 필요한 교차 출처 격리(COOP/COEP) 헤더는 CloudFront 응답 헤더 정책으로 적용

### ⭐️ 아두이노
- 가상 보드 시뮬레이션 · 회로도 · 시리얼 모니터(통신 속도 · 상태 배지)
- Web Serial로 실제 UNO 보드 연결 후 업로드
- 아두이노 에디터 자동 완성 · 문법 하이라이트

### ⭐️ COS · COS PRO 자격증
- Blockly 기반 블록코딩 실기 환경(무대 · 스프라이트 · 블록 팔레트)과 회차별 모의고사, 제출 즉시 채점
- COS PRO 문제 은행(Python · C, 1~4급 · 급수별 4세트)

### ⭐️ AI 학습 도우미
- 별도 Lambda에서 Amazon Bedrock 스트리밍 응답 (첫 글자 약 0.65초)
- 정답 코드 노출 차단: 응답 필터 + 모델 기반 정답 판정(Qwen3-32B)
- DynamoDB로 학생별 일일 사용량 한도와 질문 기록, 선생님은 반 전체 질문 기록 조회

### ⭐️ AI 학습 보고서
- 학생의 제출 · 강의실 · 과제 기록을 근거로 Bedrock(Claude Sonnet 4.6)이 학부모용 학습 보고서 작성, 인쇄 · PDF 저장
- API Gateway HTTP API의 30초 제한 때문에 **작업 접수 → DynamoDB Streams → worker Lambda → 결과 조회**로 비동기화
- worker는 VPC 밖에서 DB 자격 증명 없이 실행 (근거 스냅숏은 S3로 전달)

### ⭐️ AI 사용 의심 신호
- 제출할 때마다 코드 스타일 · 해답 뱅크 지문 · 또래 분포를 비교해 의심도를 1~3ms 안에 계산, 과제 관리 화면에 표시
- 해답 생성 · 지문화 · 또래 분포 · 소급 채점은 로컬 전용 오프라인 파이프라인(`signals/`)에서 만들어 올림

### ⭐️ 문제 · 과제 운영
- 엑셀 템플릿으로 문제를 대량 등록하는 스테이징 흐름(검증 → 수정 → 실제 채점 → 등록)
- 반 전체 또는 학생 선택 배정, 수업(classwork) · 숙제(homework) 구분, 서버 측 검색 · 필터 · 정렬 · 무한 스크롤

<details>
<summary><b>V1 주요 기능</b></summary>

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

</details>

---

## 인프라: Render → ECS → Lambda

### 변천 요약

| 시기 | 구성 | 바꾼 이유 |
| --- | --- | --- |
| **V1** (~2026.09) | Render Web Service + Supabase PostgreSQL (서울 pooler) | 무료 · 저비용으로 빠르게 출시 |
| **2026.09.19** | AWS 도쿄 리전 **ECS Fargate(Express Mode) + ALB + RDS PostgreSQL 17** + Bedrock | AI 기능(Bedrock)과 DB를 같은 AWS 안에 두고 운영 안정성 확보 |
| **2026.11.04** | **AWS Lambda(SnapStart) + API Gateway HTTP API + CloudFront/S3**, RDS 유지 | 사용량에 비해 상시 실행 비용이 너무 큼 (아래) |
| **2026.11.10** | ECS · ALB · 탄력적 IP · ECR · 보안 그룹 등 ECS 잔여 자원 삭제 | Lambda 운영 안정화 확인 후 정리 |

### 왜 ECS에서 Lambda로 바꿨나

이 서비스의 실제 사용 규모는 **최대 동시 접속 약 10명, 주간 이용 약 30명**입니다. 그런데 ECS 구성은 요청이 없어도 24시간 돌아가는 자원이 대부분이었습니다.

**2026년 10월 AWS 사용료 (크레딧 · 환급 · 세금 제외, Cost Explorer)**

| 서비스 | 10월 사용료 | 내용 |
| --- | ---: | --- |
| ECS Fargate | $22.96 | 0.5 vCPU · 1GB 태스크 1개 상시 실행 |
| RDS | $21.74 | PostgreSQL 17 `db.t4g.micro`, gp3 20GiB |
| VPC | $21.59 | 공인 IPv4 약 $11.18 + Bedrock 인터페이스 엔드포인트 약 $10.42 |
| ALB | $18.11 | 거의 시간 요금 (LCU 사용은 $0.03) |
| 기타 | $0.72 | Route 53 · ECR · Bedrock 토큰 등 |
| **합계** | **$85.12** | |

- 같은 기간 ECS CPU 평균 **0.31%**, 메모리 평균 **14%** — 자원의 대부분이 놀고 있었습니다.
- Fargate · ALB · VPC 세 항목이 **$62.66(73.6%)**. AI 호출이나 이미지 저장이 아니라 **적은 요청을 처리하려고 경로를 24시간 켜 둔 구조**가 비용의 원인이었습니다.
- 채점은 이미 브라우저에서 하고 있어서 서버는 짧은 API · DB 작업만 합니다. 요청이 있을 때만 실행되는 Lambda에 잘 맞는 부하였습니다.

**전환할 때 고려한 것**

| 문제 | 해결 |
| --- | --- |
| Lambda 콜드 스타트 | API 함수에 **SnapStart** 적용 (복원 약 0.4초). 24시간 Provisioned Concurrency는 비용 때문에 제외 |
| HTTP API 30초 제한 (AI 보고서는 최대 60초) | 보고서를 **DynamoDB 작업 + Streams + worker Lambda** 비동기 구조로 변경 |
| Bedrock 인터페이스 엔드포인트 시간 요금 | AI 함수(도우미 · 보고서 worker)를 **VPC 밖**에 두고 DB 자격 증명을 주지 않음 → 엔드포인트 제거 |
| 서버 기동 시 시드 · 마이그레이션 | 배포마다 한 번 실행하는 **migration Lambda**로 분리, 실패하면 트래픽 전환 안 함 |
| 10MB 엑셀 · 교안 업로드 | S3로 직접 업로드하는 티켓 방식으로 변경 |
| 계정 Lambda 동시성 한도 10 | 도쿄 리전 동시성 증액 요청 후 전환 |

### 전환 결과 (2026.11.25 기준 실측)

**비용 — 월 약 $85 → 약 $29 (약 66% 절감)**

| 기간 | 사용료 | 비고 |
| --- | ---: | --- |
| 2026.10 (ECS 전체 월) | $85.12 | |
| 2026.11.11 ~ 11.24 (ECS 삭제 후 14일) | $13.37 | 하루 $0.83 ~ $1.20 |
| → **30일 환산** | **약 $28.66** | RDS $22.30 · Lambda $3.96 · Bedrock 약 $1.52 · 기타 약 $0.88 |

이제 비용의 약 78%는 RDS입니다. 컴퓨팅 비용은 사용한 만큼만 나옵니다.

**안정성 — 운영 API (API Gateway, 2026.11.08 ~ 11.24)**

| 지표 | 값 |
| --- | --- |
| 요청 수 | 47,843건 |
| 5xx | **14건 (0.03%)** — 11.10 배포 중 12건, 11.13 2건, 그 외 모든 날 0건 |
| 응답 시간 p50 | 약 0.14초 |
| 응답 시간 p95 | 기간 전체 약 4.1초. 날짜별로는 0.4 ~ 1.6초. 느린 요청은 아직 원인을 분석 중 |

**운영하면서 만난 문제와 해결**

| 날짜 | 문제 | 원인 | 해결 |
| --- | --- | --- | --- |
| 11.04 | 30명 동시 접속 시험에서 3초 이내 성공 62.5% | 계정 동시성 한도 10에 걸린 503 스로틀 (성공한 요청은 빠름) | 동시성 증액. 30초에 걸쳐 분산 접속하면 100% 성공 |
| 11.04 | 첫 화면 카테고리 조회 교착 | 연결 풀 1개에서 같은 요청이 연결 2개를 요구 | 조회 경로 수정 |
| 11.07 | 수업 시작 몰림에 5xx 832건 | Lambda 실행 환경 60여 개가 동시에 복원되며 DB 연결이 1분 안에 4개 → 70개 (`too many clients`) | 요청이 끝나면 연결을 닫는 NullPool, 연결 한도 시 최대 8초 흩뜨려 재시도, 그래도 실패하면 503 + `Retry-After`. 이후 5xx 거의 0건 |
| 11.05 | 한 화면이 동시성을 혼자 씀 | 탭 하나가 API를 한꺼번에 많이 호출 | 탭별 동시 API 요청을 3개로 제한 |
| 11.10 | SnapStart 보관료가 배포마다 쌓임 | 발행 버전마다 스냅숏 보관료 | 배포 후 옛 버전 자동 삭제 (운영은 롤백용 직전 1개만 유지), staging은 SnapStart 끔 |

---

## 아키텍처와 디렉토리 구조

### 현재 운영 구조 (AWS 도쿄 리전)

```mermaid
flowchart LR
    U["학생 · 선생님 브라우저<br/>(Pyodide · clang · avr-gcc WASM 채점)"] --> CF["CloudFront<br/>agits.co.kr<br/>COOP/COEP 헤더"]
    CF --> WEB[("S3 웹 버킷<br/>SPA · WASM · 영상")]
    CF --> DATA[("S3 데이터 버킷<br/>교안 이미지 · 업로드")]
    CF --> API["API Gateway<br/>HTTP API"]
    CF --> AS["assistant Lambda<br/>AI 학습 도우미"]
    API --> L["api Lambda<br/>FastAPI · SnapStart · VPC"]
    L --> RDS[("RDS PostgreSQL 17")]
    L --> DDB[("DynamoDB<br/>보고서 · 변환 작업")]
    DDB -- Streams --> RW["report-worker Lambda"]
    DDB -- Streams --> CV["converter Lambda<br/>LibreOffice + PyMuPDF"]
    RW --> BR["Amazon Bedrock"]
    AS --> BR
    AS --> DDB2[("DynamoDB<br/>사용량 · 질문 기록")]
    RW --> DATA
    CV --> DATA
    MG["migration Lambda<br/>Alembic · 시드"] --> RDS
```

| Lambda 함수 | VPC | 메모리 | 역할 |
| --- | :---: | ---: | --- |
| `api` | 연결 | 512MB | 기존 FastAPI 전체, SnapStart |
| `report-worker` | 미연결 | 512MB | AI 학습 보고서 생성 (DB 자격 증명 없음) |
| `assistant` | 미연결 | 512MB | AI 학습 도우미 스트리밍 |
| `converter` | 미연결 | 3,008MB | 교안 PPT · PDF → 페이지 이미지 (컨테이너 이미지) |
| `migration` | 연결 | 2,048MB | 배포마다 Alembic 마이그레이션 · 시드 1회 실행 |

### CI/CD와 브랜치

- 작업 브랜치 → `dev` PR → `stage`(staging.agits.co.kr 자동 배포) → `main`(운영 배포)
- 바뀐 영역(backend · assistant · web)만 골라 테스트 · 배포
- 배포 순서: 패키지 → foundation 스택 → migration → application 스택 → SnapStart 확인 → 옛 버전 정리 → 웹 → 검증
- dev 푸시 때 stage PR 자동 생성, PR 규칙 · 병합 검사 · 직접 push 차단 · 이슈 라벨 · 프로젝트 보드 연동 워크플로

### 디렉토리 구조 (V2)

```bash
├── .github/workflows       : CI · Lambda 배포(staging/production) · PR 규칙 등 14종
├── infra/lambda            : SAM 템플릿 (foundation · application), 배포 역할 정책
├── scripts                 : Lambda 배포 · 릴리스 확인 · 마이그레이션 · 부하 시험 · DB 유휴 연결 관리
├── backend : FastAPI API 서버 (Lambda api · migration 함수)
│   ├── app
│   │   ├── main.py · lambda_api.py · snapstart_hooks.py : 앱 · Lambda 진입점 · SnapStart 복원 훅
│   │   ├── db.py · migration_handler.py · timeutils.py
│   │   ├── models.py · report_models.py           : SQLModel 데이터 모델 (테이블 43개)
│   │   ├── api                                    : 라우터 (auth · users · classrooms · problem · problem_drafts
│   │   │                                            · assignments · submissions · dashboard · learning · cos
│   │   │                                            · reports · report_jobs · assistant · arduino · public · meta)
│   │   ├── services                               : DB 쿼리 · 트랜잭션 계층, S3 · DynamoDB 클라이언트
│   │   ├── signals                                : AI 사용 의심 신호 엔진
│   │   ├── cospro · learning_seed*.py · data      : COS PRO 문제 은행 · 강의실 커리큘럼 시드
│   │   └── report_worker.py                       : AI 보고서 worker Lambda
│   ├── migrations                                 : Alembic 마이그레이션
│   └── tests                                      : pytest
├── assistant : AI 학습 도우미 Lambda (Bedrock · DynamoDB 사용량 · 정답 차단)
├── converter : 교안 변환 Lambda 컨테이너 (LibreOffice · PyMuPDF · 한글 글꼴)
├── signals   : AI 의심 신호 오프라인 파이프라인 (로컬 전용)
├── tools/arduino : 아두이노 커리큘럼 · 컴파일러 도구
├── frontend : React + Vite 웹 앱
│   └── src
│       ├── views       : 역할별 화면 (public · classroom · assignments · problems · reports · teacher-progress …)
│       ├── judge       : 브라우저 채점 엔진 (Pyodide · clang wasm · WASI)
│       ├── arduino     : 가상 보드 · avr-gcc wasm 컴파일러 · 시리얼 모니터
│       ├── cert        : COS 블록코딩(Blockly) · COS PRO
│       ├── components  : 공통 UI · AI 도우미 위젯
│       ├── hooks · app · guide · styles
├── docs     : Lambda 전환 분석 · 배포 플레이북 · 운영 기록
└── desktop  : Electron 셸 (V1 유산, 현재 미사용)
```

---

## 시작 가이드

### Requirements
- [Python 3.12](https://www.python.org/downloads/release/python-3120/) (3.10 이상 지원)
- [Node.js 20](https://nodejs.org/en/blog/release/v20.11.0)
- [npm 10](https://www.npmjs.com/package/npm/v/10.2.4)

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
> 기본 로컬 DB는 SQLite 파일입니다. 확인: `http://127.0.0.1:8000/health` · `http://127.0.0.1:8000/docs`

#### Frontend
```
$ npm install
$ npm run dev:frontend
```
> 개발 서버는 `http://localhost:5173`, API는 `/api`로 호출합니다. 다른 백엔드를 바라보려면 `frontend/.env`에 `VITE_API_BASE_URL`을 설정하세요.

#### 배포
> 운영 · staging 배포는 GitHub Actions(`lambda-staging.yml` · `lambda-production.yml`)가 수행합니다. 수동 절차는 `docs/lambda/DEPLOY_PLAYBOOK.md`를 따릅니다.

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
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=Docker&logoColor=white)

### Development
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=FastAPI&logoColor=white)
![SQLModel](https://img.shields.io/badge/SQLModel-7E56C2?style=for-the-badge&logo=SQLAlchemy&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=TypeScript&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![WebAssembly](https://img.shields.io/badge/WebAssembly-654FF0?style=for-the-badge&logo=WebAssembly&logoColor=white)
![Blockly](https://img.shields.io/badge/Blockly-4285F4?style=for-the-badge&logo=Google&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00878F?style=for-the-badge&logo=Arduino&logoColor=white)

### AWS & Database
![AWS Lambda](https://img.shields.io/badge/AWS%20Lambda-FF9900?style=for-the-badge&logo=AWS%20Lambda&logoColor=white)
![Amazon CloudFront](https://img.shields.io/badge/CloudFront-8C4FFF?style=for-the-badge&logo=Amazon%20Web%20Services&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3-569A31?style=for-the-badge&logo=Amazon%20S3&logoColor=white)
![Amazon DynamoDB](https://img.shields.io/badge/DynamoDB-4053D6?style=for-the-badge&logo=Amazon%20DynamoDB&logoColor=white)
![Amazon Bedrock](https://img.shields.io/badge/Bedrock-01A88D?style=for-the-badge&logo=Amazon%20Web%20Services&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=PostgreSQL&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=SQLite&logoColor=white)

### Test
![Pytest](https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=Pytest&logoColor=white)
