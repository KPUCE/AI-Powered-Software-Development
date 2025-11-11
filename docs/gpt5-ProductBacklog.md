좋아요. 이제 **FreeDivingLog 전체 시스템(Watch Ultra 2 + iPhone + Backend)** 을 대상으로
Scrum Framework의 **Product Backlog** 형태로 정리해줄게요.

✅ 원칙

* **Epic → Feature → User Story** 형태
* 각 User Story는 Scrum 형식인
  **“As a [user], I want to [기능], so that I can [가치].”**
* Acceptance Criteria(AC) 포함
* 플랫폼(Watch / iPhone / Backend) 별 정리

---

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

원하시면 다음 단계도 만들어드릴 수 있어요 ✅

* **우선순위(Priority / MoSCoW / RICE) 정렬된 Product Backlog**
* **Sprint 1~4 Sprint Backlog 구성**
* **Burndown Chart 템플릿**
* **Scrum Roles + Agile Ceremony 구조**

어떤 걸 이어서 진행할까요?
