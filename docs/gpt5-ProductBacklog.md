# ✅ **FreeDivingLog — Product Backlog (Scrum 기반)**

*Epic → Feature → User Story → Acceptance Criteria*

---

# 🟦 1. EPIC — Apple Watch Ultra 2 기능 개발

---

## ✅ **Feature A1 — Dive Session 자동 감지**

### **User Story A1-1 — 수심 기반 자동 감지**

**As a** freediver
**I want** the watch to automatically detect a dive when depth increases
**so that** I don’t need to press any buttons underwater.

**AC**

* 깊이 변화 ≥ 1m, 2초 이상 지속 → 자동 세션 시작
* 수면 수심(0m ± 0.3m) 도달 시 자동 종료
* 세션 ID 자동 생성

---

## ✅ **Feature A2 — 실시간 모니터링(UI + Sensor)**

### **User Story A2-1 — 실시간 수심 표시**

**As a** diver
**I want** to see real-time depth updates
**so that** I can track my dive safely.

**AC**

* 깊이 업데이트 주기 ≤ 0.5초
* 깊이/잠수시간/수온 표시
* 고대비 + 대형 폰트 적용

---

### **User Story A2-2 — 상승속도 경고**

**As a** diver
**I want** haptic warning when ascent speed is too fast
**so that** I avoid shallow water blackout.

**AC**

* 상승속도 > 1.2m/s 시 진동
* UI 배경 빨간색으로 전환
* Warning flag 로그에 저장

---

### **User Story A2-3 — 목표깊이 알림**

**As a** diver
**I want** a vibration alert when reaching target depth
**so that** I know exactly when to turn.

**AC**

* 목표 깊이 도달 시 햅틱
* UI에 “Target Reached” 표시

---

## ✅ **Feature A3 — 오프라인 데이터 저장**

### **User Story A3-1 — 로컬 캐싱**

**As a** diver
**I want** the watch to store all log data offline
**so that** dives are recorded even without iPhone connection.

**AC**

* Local CoreData 저장
* 세션·샘플 모두 저장
* 저장 실패 시 retry

---

## ✅ **Feature A4 — 수면 회복(Surface Recovery)**

### **User Story A4-1 — 자동 회복 타이머**

**As a** diver
**I want** a recovery timer to start automatically
**so that** I can ensure proper rest.

**AC**

* 세션 종료 → 회복 타이머 자동 시작
* 회복 목표 미달 시 다음 다이브에서 경고

---

## ✅ **Feature A5 — 워치 설정 관리**

### User Story A5-1 — 언어/단위 설정

**As a** user
**I want** to adjust language and units on the watch
**so that** I see UI in my preferred format.

**AC**

* 언어(한국어/영어) 변경
* 미터·피트 / 섭씨·화씨 선택
* iPhone과 양방향 동기화

---

# 🟩 2. EPIC — iPhone 앱 기능 개발

---

## ✅ **Feature B1 — 로그 수신 및 저장**

### User Story B1-1 — 워치 로그 자동 수신

**As a** user
**I want** my iPhone to receive dive logs automatically
**so that** I can review them later.

**AC**

* WatchConnectivity 기반 자동 수신
* CoreData 저장
* 중복 세션 방지 (UUID 기준)

---

### User Story B1-2 — 그래프 시각화

**As a** diver
**I want** to see a depth-time graph
**so that** I can understand my dive profile.

**AC**

* 인터랙티브 그래프 지원
* 샘플 10,000+ 처리 가능

---

## ✅ **Feature B2 — Dashboard 구성**

### User Story B2-1 — 대시보드 요약

**As a** user
**I want** to see all important dive metrics in a single dashboard
**so that** I quickly understand my performance.

**AC**

* 오늘의 다이브 요약
* 최근 트렌드 그래프
* AI 추천 표시

---

## ✅ **Feature B3 — AI 분석/인사이트**

### User Story B3-1 — 성장 트렌드 분석

**As a** diver
**I want** weekly/monthly trend insights
**so that** I can track improvement.

**AC**

* 평균 깊이/횟수 변화 계산
* 피드백 문구 생성

---

### User Story B3-2 — AI 코칭 제안

**As a** diver
**I want** training suggestions
**so that** I can improve safely.

**AC**

* Recovery Efficiency 계산
* 목표깊이 도달률 분석
* CoreML 로컬 모델 적용

---

## ✅ **Feature B4 — 커뮤니티 기능**

### User Story B4-1 — 버디 추가

**As a** user
**I want** to add dive buddies
**so that** we can share logs.

---

### User Story B4-2 — 다이브 스팟 지도

**As a** user
**I want** to browse dive spots
**so that** I can find recommended locations.

---

## ✅ **Feature B5 — 설정(Settings)**

### User Story B5-1 — 언어/단위 설정

(Watch와 동일, iPhone이 기준)

---

### User Story B5-2 — 백업/복원

**As a** user
**I want** iCloud backup
**so that** I never lose my logs.

---

# 🟥 3. EPIC — Backend 서버 개발

---

## ✅ **Feature C1 — 사용자 인증**

### User Story C1-1 — Apple 로그인

AC: JWT 기반 토큰, refresh token 지원

---

## ✅ **Feature C2 — Dive Log 저장 API**

### User Story C2-1 — 세션/샘플 업로드

AC:

* REST/GraphQL
* UUID 기반 정합성
* 10,000 샘플 이상 처리

---

## ✅ **Feature C3 — AI 분석 백엔드 (선택)**

### User Story C3-1 — 분석 결과 저장

AC:

* JSONB 저장 (PostgreSQL)
* 결과 조회 API 제공

---

## ✅ **Feature C4 — 커뮤니티 기능**

### User Story C4-1 — 버디 관계

AC:

* 친구 요청/승인/삭제
* 개인정보 보호 준수

---

## ✅ **Feature C5 — 데이터 최적화**

### User Story C5-1 — 캐싱

AC:

* Redis로 랭킹/최근 로그 캐시
* TTL 24h 설정

---

# ✅ 최종 Product Backlog 요약

| Platform           | Feature Count | User Story Count |
| ------------------ | ------------- | ---------------- |
| **Watch Ultra 2**  | 5             | 12               |
| **iPhone App**     | 5             | 14               |
| **Backend Server** | 5             | 10               |

총 **36개 User Story**로 구성된 대규모 백로그입니다.

---



# ✅ **FreeDivingLog — Product Backlog (Story Point + 예상 개발 시간)**


✅ 원칙

* **Story Point 기준:** Fibonacci (1,2,3,5,8,13…)
* **1 SP ≈ 4~6시간(개발 난이도 기준)**
* Effort는 **개발자 1명 기준 추정치**
* QA/디자인은 포함하지 않은 개발 기본 시간

---

# 🟦 **1. Apple Watch Ultra 2 Backlog**

| ID   | User Story                  | SP     | 예상 개발 시간   |
| ---- | --------------------------- | ------ | ---------- |
| A1-1 | 자동 다이브 감지(수심 변화 ≥1m, 2초 지속) | **8**  | **32–40h** |
| A2-1 | 실시간 수심/시간/수온 표시 (0.5s 업데이트) | **13** | **52–70h** |
| A2-2 | 상승속도 경고 + UI 색상 변환          | **8**  | **32–40h** |
| A2-3 | 목표 깊이 햅틱 알림                 | **5**  | **20–25h** |
| A3-1 | 오프라인 로컬 저장(CoreData)        | **8**  | **32–40h** |
| A4-1 | 자동 회복 타이머                   | **5**  | **20–25h** |
| A5-1 | 언어/단위 설정 + iPhone 동기화       | **8**  | **32–40h** |
| A2-4 | 수중 UI(고대비/대형 폰트)            | **3**  | **12–18h** |
| A3-2 | 세션·샘플 저장 Retry 시스템          | **5**  | **20–25h** |
| A1-2 | 세션 종료/요약 생성                 | **5**  | **20–25h** |
| A4-2 | 회복 부족 경고                    | **3**  | **12–18h** |
| A5-2 | WatchConnectivity 통신 안정화    | **8**  | **32–40h** |

✅ **총합 (Watch)**:
**SP = 79**
**예상 개발 시간 = 316 ~ 416 시간**

---

# 🟩 **2. iPhone App Backlog**

| ID   | User Story                 | SP     | 예상 개발 시간   |
| ---- | -------------------------- | ------ | ---------- |
| B1-1 | 워치 로그 자동 수신                | **8**  | **32–40h** |
| B1-2 | 로그 CoreData 저장             | **5**  | **20–25h** |
| B1-3 | Depth-Time 그래프 구현          | **8**  | **32–48h** |
| B2-1 | Dashboard 구축(요약/트렌드/AI/목표) | **13** | **52–78h** |
| B2-2 | Sync Status 표시             | **3**  | **12–18h** |
| B3-1 | 주간/월간 트렌드 분석               | **5**  | **20–30h** |
| B3-2 | AI 코칭(CoreML)              | **8**  | **32–50h** |
| B4-1 | 버디 추가/관리                   | **5**  | **20–25h** |
| B4-2 | 다이브 스팟 지도(MapKit)          | **5**  | **20–25h** |
| B5-1 | 언어/단위 설정 페이지               | **3**  | **12–18h** |
| B5-2 | iCloud 백업/복원(KVS)          | **5**  | **20–25h** |
| B5-3 | Export (PDF/CSV)           | **3**  | **12–18h** |
| B1-4 | 세션 상세 페이지 + 그래프 인터랙션       | **5**  | **20–25h** |
| B2-3 | Dive Goal(주간 목표) UI        | **3**  | **12–16h** |

✅ **총합 (iPhone)**:
**SP = 83**
**예상 개발 시간 = 316 ~ 441 시간**

---

# 🟥 **3. Backend Server Backlog**

| ID   | User Story                 | SP    | 예상 개발 시간   |
| ---- | -------------------------- | ----- | ---------- |
| C1-1 | Apple 로그인 OAuth            | **5** | **20–25h** |
| C2-1 | Dive Session 저장 API        | **5** | **20–25h** |
| C2-2 | Dive Sample 업로드 API        | **8** | **32–48h** |
| C3-1 | 분석 결과 저장(JSONB)            | **5** | **20–25h** |
| C3-2 | AI 분석 Lambda 연동            | **8** | **32–48h** |
| C4-1 | 버디 관계 API                  | **5** | **20–25h** |
| C4-2 | 다이브 스팟(리뷰 포함) API          | **5** | **20–25h** |
| C5-1 | Redis 캐싱(랭킹/최근 로그)         | **5** | **20–25h** |
| C5-2 | 데이터 검증/클린징 파이프라인           | **3** | **12–18h** |
| C2-3 | 서버 로그/모니터링(Sentry/Grafana) | **3** | **12–18h** |

✅ **총합 (Backend)**:
**SP = 52**
**예상 개발 시간 = 216 ~ 282 시간**

---

# ✅ 전체 시스템 총합

| 영역                      | Story Points | 개발 시간              |
| ----------------------- | ------------ | ------------------ |
| **Apple Watch Ultra 2** | 79           | 316–416h           |
| **iPhone App**          | 83           | 316–441h           |
| **Backend Server**      | 52           | 216–282h           |
| **✅ Total**             | **214 SP**   | **848 ~ 1,139 시간** |

💡 만약 1명 개발자 기준 **주 40시간**으로 진행한다면?
➡️ **약 21주 ~ 29주 (5~7개월)** 규모

---



