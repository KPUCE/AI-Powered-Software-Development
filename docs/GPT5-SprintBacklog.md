# ✅ ⭐ 전체 스프린트 로드맵 요약 (핵심 중심 ✅ → 확장 🔄 → 고도화 🤖)

| Sprint | 기간          | 목표                            | 상태       |
| ------ | ----------- | ----------------------------- | -------- |
| **1**  | 1/2 ~ 1/15  | 다이브 자동 감지 + 실시간 모니터링(워치 MVP)  | ✅ 핵심     |
| **2**  | 1/16 ~ 1/29 | 워치 로그 저장 + iPhone 동기화         | ✅ 핵심     |
| **3**  | 1/30 ~ 2/12 | iPhone Logbook + 그래프 + 세션 상세  | ✅ 핵심     |
| **4**  | 2/13 ~ 2/26 | Dashboard + AI 기초 분석          | 🔄 기능 확장 |
| **5**  | 2/27 ~ 3/12 | Backend API + iCloud + 설정 동기화 | 🔄 기능 확장 |
| **6**  | 3/13 ~ 3/26 | 커뮤니티(버디/스팟) + Export          | 🤖 고도화   |

---

# ✅ Sprint Backlog 상세표

(각 Sprint는 2주이며, Story Point 총합이 약 **35~40 SP 범위**가 되도록 구성함)

---

# ✅ **Sprint 1 — 핵심 센서·다이브 감지 기능 (Watch MVP)**

📆 **2026년 1월 2일 ~ 1월 15일 (2주)**
🎯 목표: *워치 단독으로 “다이빙 자동 감지 + 실시간 UI”가 동작하는 첫 MVP*

| Story ID | 내용                    | SP        |
| -------- | --------------------- | --------- |
| A1-1     | 자동 다이브 감지(≥1m/2초)     | 8         |
| A2-1     | 실시간 수심/시간/수온 표시(0.5s) | 13        |
| A2-2     | 상승속도 경고(UI+햅틱)        | 8         |
| A2-3     | 목표깊이 알림               | 5         |
| A2-4     | 수중 고대비 UI 구성          | 3         |
| **총합**   |                       | **37 SP** |

✅ **Sprint 1 종료일: 2026년 1월 15일**

---

# ✅ **Sprint 2 — 로컬 저장 + 워치↔iPhone 동기화 기능**

📆 **2026년 1월 16일 ~ 1월 29일**
🎯 목표: *세션이 저장되고, iPhone으로 동기화되는 완전 데이터 흐름 구현*

| Story ID | 내용                       | SP        |
| -------- | ------------------------ | --------- |
| A3-1     | 워치 로컬 저장(CoreData)       | 8         |
| A3-2     | 세션/샘플 저장 retry 시스템       | 5         |
| A1-2     | 세션 종료 후 요약 생성            | 5         |
| A4-1     | 자동 회복 타이머                | 5         |
| A5-2     | WatchConnectivity 통신 안정화 | 8         |
| B1-1     | iPhone 로그 자동 수신          | 8         |
| **총합**   |                          | **39 SP** |

✅ **Sprint 2 종료일: 2026년 1월 29일**

---

# ✅ **Sprint 3 — iPhone Logbook + 그래프 시각화**

📆 **2026년 1월 30일 ~ 2월 12일**
🎯 목표: *기본적인 다이빙 기록 조회 + 그래프 기반 분석 가능*

| Story ID | 내용              | SP        |
| -------- | --------------- | --------- |
| B1-2     | CoreData에 로그 저장 | 5         |
| B1-3     | Depth-Time 그래프  | 8         |
| B1-4     | 세션 상세 페이지       | 5         |
| B2-1     | 대시보드 요약 기본 버전   | 13        |
| B2-3     | Dive Goal UI    | 3         |
| **총합**   |                 | **34 SP** |

✅ **Sprint 3 종료일: 2026년 2월 12일**

---

# ✅ **Sprint 4 — Dashboard + AI 기초 분석 (Local ML)**

📆 **2026년 2월 13일 ~ 2월 26일**
🎯 목표: *대시보드 완성 + AI 추천 기본 구조*

| Story ID | 내용                  | SP                        |
| -------- | ------------------- | ------------------------- |
| B2-2     | Sync Status UI      | 3                         |
| B3-1     | 주간/월간 트렌드 분석        | 5                         |
| B3-2     | AI 코칭(기초 모델 CoreML) | 8                         |
| A4-2     | 회복 부족 경고            | 3                         |
| B2-1-ext | 대시보드 고급 그래프/요약      | 5                         |
| C3-1     | 분석 결과 저장(JSONB)     | 5                         |
| **총합**   |                     | **29 SP** (조금 가벼운 Sprint) |

✅ **Sprint 4 종료일: 2026년 2월 26일**

---

# ✅ **Sprint 5 — Backend API + 설정 동기화 + iCloud 통합**

📆 **2026년 2월 27일 ~ 3월 12일**
🎯 목표: *외부 서버/클라우드 연동 기능을 구축하여 서비스 기반 강화*

| Story ID | 내용                  | SP        |
| -------- | ------------------- | --------- |
| C1-1     | Apple 로그인           | 5         |
| C2-1     | Dive Session 저장 API | 5         |
| C2-2     | Dive Sample 저장 API  | 8         |
| B5-1     | 언어/단위 설정 페이지        | 3         |
| B5-2     | iCloud 동기화(KVS)     | 5         |
| A5-1     | 워치 언어/단위 설정 + 동기화   | 8         |
| **총합**   |                     | **34 SP** |

✅ **Sprint 5 종료일: 2026년 3월 12일**

---

# ✅ **Sprint 6 — 커뮤니티 + Export + 서버 고도화**

📆 **2026년 3월 13일 ~ 3월 26일**
🎯 목표: *커뮤니티·스팟 기능 및 PDF/CSV 내보내기 등 확장 기능 완성*

| Story ID | 내용               | SP        |
| -------- | ---------------- | --------- |
| B4-1     | 버디 추가/관리         | 5         |
| B4-2     | 다이브 스팟 지도        | 5         |
| B5-3     | Export (PDF/CSV) | 3         |
| C4-1     | 버디 관계 API        | 5         |
| C4-2     | 스팟 데이터 API       | 5         |
| C5-1     | Redis 캐싱         | 5         |
| C5-2     | 데이터 검증/클린징       | 3         |
| **총합**   |                  | **31 SP** |

✅ **Sprint 6 종료일: 2026년 3월 26일**

---

# ✅ 전체 Sprint 종료일 요약

| Sprint | 기간          | 종료일      |
| ------ | ----------- | -------- |
| **1**  | 1/2 ~ 1/15  | ✅ 1월 15일 |
| **2**  | 1/16 ~ 1/29 | ✅ 1월 29일 |
| **3**  | 1/30 ~ 2/12 | ✅ 2월 12일 |
| **4**  | 2/13 ~ 2/26 | ✅ 2월 26일 |
| **5**  | 2/27 ~ 3/12 | ✅ 3월 12일 |
| **6**  | 3/13 ~ 3/26 | ✅ 3월 26일 |

📌 **전체 프로젝트 예상 종료일 → 2026년 3월 26일**

---
# User Story에서 Tsk로의 변환

# ✅ **1. Apple Watch Ultra 2 — User Story → Task 변환**

---

## ✅ **A1-1 자동 다이브 감지**

**User Story:** 수심 증가(≥1m, 2초 지속) 시 자동 Dive Start 감지

### ✅ Tasks

1. 수심 센싱용 CoreMotion/Depth API 초기 세팅
2. 센서 스트림(0.5초 간격) Listener 구현
3. 깊이 변화 필터링(노이즈 제거 알고리즘)
4. Dive Start 조건 검사 로직 구현
5. Dive End(0m ±0.3m) 감지 로직
6. Dive Session 객체 생성 + startTime 기록
7. 감지 이벤트 Unit Test 작성
8. 실제 워치 테스트 (수중 시뮬레이터 또는 압력 테스트기)

---

## ✅ **A2-1 실시간 수심/시간/수온 표시**

### ✅ Tasks

1. 실시간 센서 데이터 모델 정의
2. Combine 기반 실시간 업데이트 파이프 구현
3. 0.5s UI 업데이트 간격 구현 (throttle)
4. 고대비/대형 폰트 UI 컴포넌트 제작
5. 워치 화면 레이아웃 제작 (SwiftUI)
6. 성능 최적화(메모리/배터리 모니터링)
7. Watch에서 live preview 테스트

---

## ✅ **A2-2 상승속도 경고**

### ✅ Tasks

1. ascentSpeed = Δdepth/Δtime 계산
2. 임계값(1.2m/s) 비교 로직 구현
3. 경고 발생 시 햅틱 트리거
4. UI 배경 Red 전환 애니메이션
5. 경고 이벤트 로그 저장
6. Unit Test: 상승속도 시나리오

---

## ✅ **A2-3 목표 깊이 알림**

### ✅ Tasks

1. 사용자 설정값 Sync 받기
2. 목표깊이 비교 로직 구현
3. 도달 시 햅틱 제공
4. UI에 Target Reached 표시
5. 로그 플래그 저장

---

## ✅ **A2-4 수중 고대비 UI**

### ✅ Tasks

1. 고대비 컬러팔레트 정의
2. 대형 SF 폰트 스타일 정의
3. 수중에서 시인성 테스트
4. 라이트/다크 모드 무시하도록 설정

---

## ✅ **A3-1 로컬 저장(CoreData)**

### ✅ Tasks

1. DiveSession / DiveSample 모델 정의
2. CoreData Schema 생성
3. 세션 시작/종료 시 DB 저장
4. 샘플 저장(batch insert) 구현
5. 저장 실패 시 retry 큐 구현
6. 저장 로깅 및 DB 파일 무결성 테스트

---

## ✅ **A4-1 자동 회복 타이머**

### ✅ Tasks

1. surface detection → 타이머 시작 로직
2. 회복 목표값 가져오기
3. UI 타이머 구성
4. 회복 부족 경고 표시
5. 로그 기록

---

## ✅ **A5-1 언어/단위 설정**

### ✅ Tasks

1. 단위(미터/피트, °C/°F) 변환 함수 작성
2. 워치 설정 화면 SwiftUI 작성
3. iPhone → Watch 설정 Sync
4. 단위 변경 시 실시간 UI 반영

---

---

# ✅ **2. iPhone App — User Story → Task 변환**

---

## ✅ **B1-1 워치 로그 자동 수신**

### ✅ Tasks

1. WatchConnectivity Session 설정
2. 파일/메시지 수신 핸들러 구현
3. 수신 데이터(JSON) 파싱
4. duplicate session 방지 logic
5. CoreData 저장
6. 수신 완료 알림 (UX)

---

## ✅ **B1-2 CoreData 저장**

### ✅ Tasks

1. CoreData 모델 생성
2. migration 정책 자동화
3. Insert/Fetch/Update 함수 구축
4. BackgroundContext 처리
5. 저장 성능 테스트

---

## ✅ **B1-3 Depth-Time 그래프**

### ✅ Tasks

1. 그래프용 시계열 데이터 변환
2. Swift Charts/Recharts 뷰 구성
3. 터치 인터랙션(tooltip) 구현
4. 줌/스크롤 처리
5. 그래프 성능 최적화

---

## ✅ **B2-1 대시보드 기본 UI**

### ✅ Tasks

1. 오늘의 Dive Summary Section
2. 최근 7일 트렌드 그래프
3. 목표 달성 Progress Bar
4. Sync Status Panel
5. Dashboard ViewModel 결합
6. 애니메이션/Transition 적용

---

## ✅ **B3-1 트렌드 분석**

### ✅ Tasks

1. 7일·30일 Data Aggregation 함수
2. 평균 수심/횟수 계산
3. 그래프용 데이터 구조 구축
4. 결과 캐싱

---

## ✅ **B3-2 AI 코칭(CoreML)**

### ✅ Tasks

1. CoreML 모델 로딩
2. 입력 feature 생성 (recovery ratio 등)
3. 추천 문구 생성 로직
4. Dashboard와 연동
5. 모델 정확도 테스트

---

## ✅ **B4-1 버디 기능**

### ✅ Tasks

1. 사용자 검색 API 연동
2. 친구 추가/삭제 UI
3. 친구 상태 표시
4. Log 공유 권한 체크

---

## ✅ **B4-2 스팟 지도**

### ✅ Tasks

1. MapKit 초기 설정
2. 장소 마커 표시
3. 상세 정보 페이지 구성
4. 스팟 리뷰 추가

---

## ✅ **B5-1 언어/단위 설정**

### ✅ Tasks

1. Language Picker UI
2. Unit Picker UI
3. UserDefaults + iCloud Sync
4. 변경 시 전체 앱 언어 반영

---

## ✅ **B5-3 Export**

### ✅ Tasks

1. PDF 템플릿 디자인
2. CSV 변환기 개발
3. Share Sheet 연동

---

---

# ✅ **3. Backend — User Story → Task 변환**

---

## ✅ **C1-1 Apple 로그인(OAuth)**

### ✅ Tasks

1. Sign in with Apple 설정
2. 서버에서 token validation
3. 사용자 프로필 저장
4. JWT 발급 로직

---

## ✅ **C2-1 Dive Session API**

### ✅ Tasks

1. Session POST API 설계
2. Validation (depth/time)
3. DB insert
4. 응답 Schema 정의

---

## ✅ **C2-2 Dive Sample API**

### ✅ Tasks

1. Bulk insert endpoint 생성
2. 고속 insert 최적화
3. 이상치 필터링
4. 샘플 카운트 검증

---

## ✅ **C3-1 AI 분석결과 저장**

### ✅ Tasks

1. JSONB 저장 스키마 설계
2. Insert/Select API
3. 분석 Job Trigger 처리

---

## ✅ **C4-1 버디 API**

### ✅ Tasks

1. 친구 추가/승인/삭제 API
2. 친구 관계 테이블 생성
3. Permission 체크

---

## ✅ **C4-2 스팟 데이터 API**

### ✅ Tasks

1. Spot 테이블 생성
2. Review 테이블 생성
3. 목록/상세 API

---

## ✅ **C5-1 Redis 캐싱**

### ✅ Tasks

1. 캐싱 Key 구조 설계
2. 랭킹 캐싱
3. 최근 로그 캐싱
4. TTL 설정

---

## ✅ **C5-2 데이터 클린징**

### ✅ Tasks

1. 깊이 점프 이상치 제거 규칙
2. 0m 오류 샘플 처리
3. 정기 클린징 Job(Cron)

---

---

# ✅ 필요하시면 다음도 만들어드릴 수 있어요:

✅ **Sprint별 Task 보드 (칸반 형태)**
✅ **총 Task 수 & 인력 기준 소요 시간 자동 계산**
✅ **JIRA Import용 CSV**
✅ **Task 간 Dependency 맵(의존성 다이어그램)**

원하시는 걸 알려주세요!

