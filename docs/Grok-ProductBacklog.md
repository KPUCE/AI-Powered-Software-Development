## **FreeDivingLog – Scrum Product Backlog**  
**프로덕트 비전**: *Apple Watch Ultra 2 + iPhone 기반 실시간 프리다이빙 로그 & 안전 모니터링 서비스*  
**개발 프레임워크**: **Scrum** (2주 스프린트 기준)  
**플랫폼**: **watchOS 11+**, **iOS 18+**, **서버리스 백엔드 (iCloud + PostgreSQL)**  

---

## **에픽 (Epic) 분류**

| 에픽 | 설명 |
|------|------|
| **E1** | 실시간 다이빙 모니터링 (Watch) |
| **E2** | 오프라인 로그 기록 & 동기화 |
| **E3** | 데이터 분석 & 시각화 (iPhone) |
| **E4** | AI 기반 인사이트 & 코칭 |
| **E5** | 커뮤니티 & 공유 기능 |
| **E6** | 설정 & 현지화 (i18n) |
| **E7** | 백엔드 & 데이터 관리 |
| **E8** | 배포 & 운영 |

---

## **Product Backlog (우선순위 순)**  
> **우선순위 기준**: **MoSCoW (Must → Should → Could → Won’t)**  
> **Story Point**: Fibonacci (1, 2, 3, 5, 8, 13)  
> **Acceptance Criteria (AC)** 포함

---

### **E1. 실시간 다이빙 모니터링 (Watch)** – **Must**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-01 | **As a freediver**, I want **auto dive detection** when depth ≥1m for ≥2s, **so that** session starts without manual input. | Watch | 8 | - 자동 시작/종료<br>- 0.5초 주기 센서 업데이트<br>- 테스트: 1m 유지 → 시작 |
| PB-02 | **As a diver**, I want **real-time depth, time, temp display** in **large font**, **so that** I can read underwater. | Watch | 5 | - 80pt 수심, 70pt 시간<br>- 고대비 UI |
| PB-03 | **As a diver**, I want **haptic alert** when ascent speed >1.2m/s, **so that** I avoid blackout. | Watch | 5 | - 강한 진동<br>- UI 빨강 전환 |
| PB-04 | **As a diver**, I want **target depth haptic** when reached, **so that** I know without looking. | Watch | 3 | - 3회 짧은 진동 |
| PB-05 | **As a diver**, I want **surface recovery timer** with warning if < set time, **so that** I rest properly. | Watch | 5 | - 자동 타이머<br>- 부족 시 경고 |

---

### **E2. 오프라인 로그 기록 & 동기화** – **Must**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-06 | **As a user**, I want **offline log storage** on Watch, **so that** data is safe without iPhone. | Watch | 5 | - CoreData + App Group |
| PB-07 | **As a user**, I want **auto sync to iPhone** within 10s when connected, **so that** logs are up-to-date. | Watch ↔ iPhone | 8 | - WatchConnectivity<br>- 99% 성공률 |
| PB-08 | **As a user**, I want **iCloud backup**, **so that** data is restored on new device. | iPhone | 5 | - iCloudKit 자동 백업 |

---

### **E3. 데이터 분석 & 시각화 (iPhone)** – **Should**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-09 | **As a user**, I want **depth-time graph** per dive, **so that** I review profile. | iPhone | 8 | - Swift Charts<br>- 확대/축소 |
| PB-10 | **As a user**, I want **session stats**: max depth, avg, total time, count. | iPhone | 5 | - 카드 UI |
| PB-11 | **As a user**, I want **weekly/monthly trend**, **so that** I track progress. | iPhone | 8 | - 라인 차트 |

---

### **E4. AI 기반 인사이트 & 코칭** – **Could**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-12 | **As a user**, I want **AI recovery suggestion** based on rest ratio, **so that** I improve safely. | iPhone | 13 | - CoreML 모델<br>- "다음 PB 35m 가능" |
| PB-13 | **As a user**, I want **Dive Efficiency Score**, **so that** I quantify performance. | iPhone | 13 | - 심박 + 수심 + 휴식 통합 |

---

### **E5. 커뮤니티 & 공유 기능** – **Could**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-14 | **As a user**, I want **buddy log sharing**, **so that** we compare dives. | iPhone | 8 | - iCloud Private Share |
| PB-15 | **As a user**, I want **dive spot map**, **so that** I find good locations. | iPhone | 8 | - MapKit + 리뷰 |

---

### **E6. 설정 & 현지화** – **Must**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-16 | **As a user**, I want **language toggle** (KR/EN), **so that** I use in my language. | Watch + iPhone | 5 | - i18n, Localizable.strings |
| PB-17 | **As a user**, I want **unit toggle** (m/ft, °C/°F), **so that** I use preferred unit. | Watch + iPhone | 5 | - 실시간 변환 |
| PB-18 | **As a user**, I want **sync settings** via iCloud, **so that** Watch/iPhone same. | Watch ↔ iPhone | 5 | - iCloud Key-Value |

---

### **E7. 백엔드 & 데이터 관리** – **Must**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-19 | **As a developer**, I want **PostgreSQL schema** for logs, **so that** analytics run fast. | Backend | 8 | - users, sessions, dives 테이블 |
| PB-20 | **As a user**, I want **data export** (PDF/CSV), **so that** I backup externally. | iPhone | 5 | - Share Sheet |

---

### **E8. 배포 & 운영** – **Must**

| # | User Story | 플랫폼 | SP | AC |
|---|-----------|--------|----|----|
| PB-21 | **As a user**, I want **App Store release**, **so that** I download easily. | App Store | 5 | - TestFlight → Release |
| PB-22 | **As a developer**, I want **crash monitoring**, **so that** I fix bugs fast. | All | 3 | - Firebase Crashlytics |

---

## **스프린트 계획 예시 (2주 스프린트)**

| 스프린트 | 목표 | 포함 백로그 | 총 SP |
|---------|------|-------------|-------|
| **Sprint 1** | MVP: 자동 감지 + 오프라인 로그 | PB-01, PB-06, PB-07, PB-16, PB-17, PB-18 | **36** |
| **Sprint 2** | 실시간 UI + 동기화 | PB-02, PB-03, PB-04, PB-05, PB-08 | **31** |
| **Sprint 3** | iPhone 대시보드 + 그래프 | PB-09, PB-10, PB-11 | **21** |
| **Sprint 4** | AI + 백엔드 | PB-12, PB-19 | **21** |
| **Sprint 5** | 커뮤니티 + 배포 | PB-14, PB-15, PB-21, PB-22 | **29** |

---

## **Definition of Done (DoD)**

- [x] 코드 리뷰 완료 (2명 이상)  
- [x] 유닛 테스트 80% 커버리지  
- [x] UI 테스트 (Xcode Preview + 실기기)  
- [x] Watch/iPhone 동기화 테스트  
- [x] 배터리 소모 <15% (2시간 다이빙)  
- [x] 문서화 (Jira + Confluence)  
- [x] App Store 리뷰 통과 기준 충족

---

## **FreeDivingLog – Product Backlog (Story Point + 예측 시간 포함)**  
**기준**:  
- **Story Point (SP)**: Fibonacci (1, 2, 3, 5, 8, 13)  
- **예측 시간**: **1 SP = 4시간** (팀 평균 속도 기준)  
- **팀 구성**: iOS 2명, WatchOS 1명, Backend 1명, QA 1명 (총 5명)  
- **2주 스프린트 = 10일 = 80시간/명**

---

| # | **User Story** | **플랫폼** | **SP** | **예측 시간** | **담당자** | **비고** |
|---|----------------|-----------|--------|----------------|-----------|---------|
| **E1. 실시간 다이빙 모니터링 (Watch)** – **Must** |
| PB-01 | 자동 다이브 감지 (≥1m, ≥2s) | Watch | 8 | **32시간** | WatchOS | CoreMotion + 타이머 |
| PB-02 | 실시간 수심/시간/온도 대형 표시 | Watch | 5 | **20시간** | WatchOS | SwiftUI + 고대비 |
| PB-03 | 상승속도 >1.2m/s 햅틱 경고 | Watch | 5 | **20시간** | WatchOS | Haptics + 실시간 계산 |
| PB-04 | 목표 깊이 도달 시 진동 | Watch | 3 | **12시간** | WatchOS | 설정 연동 |
| PB-05 | 수면 회복 타이머 + 경고 | Watch | 5 | **20시간** | WatchOS | 타이머 + UI 피드백 |
| **소계** | | | **26** | **104시간** | | |

| **E2. 오프라인 로그 & 동기화** – **Must** |
| PB-06 | Watch 오프라인 CoreData 저장 | Watch | 5 | **20시간** | WatchOS | App Group + 모델 |
| PB-07 | Watch → iPhone 자동 동기화 (<10s) | Watch ↔ iPhone | 8 | **32시간** | WatchOS + iOS | WatchConnectivity |
| PB-08 | iCloud 자동 백업/복원 | iPhone | 5 | **20시간** | iOS | iCloudKit |
| **소계** | | | **18** | **72시간** | | |

| **E3. 데이터 분석 & 시각화 (iPhone)** – **Should** |
| PB-09 | 수심-시간 그래프 (Swift Charts) | iPhone | 8 | **32시간** | iOS | 확대/축소 + 터치 |
| PB-10 | 세션 통계 카드 (max, avg, total) | iPhone | 5 | **20시간** | iOS | 카드 UI |
| PB-11 | 주/월 트렌드 차트 | iPhone | 8 | **32시간** | iOS | 날짜 그룹화 |
| **소계** | | | **21** | **84시간** | | |

| **E4. AI 기반 인사이트** – **Could** |
| PB-12 | AI 회복비율 기반 훈련 제안 | iPhone | 13 | **52시간** | iOS + ML | CoreML 모델 |
| PB-13 | Dive Efficiency Score | iPhone | 13 | **52시간** | iOS + Backend | 심박 + 수심 통합 |
| **소계** | | | **26** | **104시간** | | |

| **E5. 커뮤니티 & 공유** – **Could** |
| PB-14 | 버디 로그 공유 (iCloud) | iPhone | 8 | **32시간** | iOS | Private Share |
| PB-15 | 다이브 스팟 지도 + 리뷰 | iPhone | 8 | **32시간** | iOS | MapKit |
| **소계** | | | **16** | **64시간** | | |

| **E6. 설정 & 현지화** – **Must** |
| PB-16 | 언어 전환 (KR/EN) | Watch + iPhone | 5 | **20시간** | iOS | i18n + Localizable |
| PB-17 | 단위 전환 (m/ft, °C/°F) | Watch + iPhone | 5 | **20시간** | WatchOS + iOS | 실시간 변환 |
| PB-18 | 설정 iCloud 동기화 | Watch ↔ iPhone | 5 | **20시간** | iOS | Key-Value Store |
| **소계** | | | **15** | **60시간** | | |

| **E7. 백엔드 & 데이터 관리** – **Must** |
| PB-19 | PostgreSQL 스키마 + API | Backend | 8 | **32시간** | Backend | users, sessions, dives |
| PB-20 | PDF/CSV 내보내기 | iPhone | 5 | **20시간** | iOS | Share Sheet |
| **소계** | | | **13** | **52시간** | | |

| **E8. 배포 & 운영** – **Must** |
| PB-21 | App Store 출시 | All | 5 | **20시간** | PM + QA | TestFlight → Release |
| PB-22 | Crashlytics 모니터링 | All | 3 | **12시간** | Backend | Firebase |
| **소계** | | | **8** | **32시간** | | |

---

## **총합 요약**

| 항목 | 값 |
|------|----|
| **총 Story Point** | **143 SP** |
| **총 예측 시간** | **572시간** (약 **72일**, 5명 기준) |
| **MVP (Must)** | **77 SP** → **308시간** → **약 8주** |
| **스프린트 수 (2주)** | **약 7~8 스프린트** |

---

## **MVP 스프린트 계획 (Must Only)**

| 스프린트 | 포함 백로그 | SP | 시간 |
|---------|-------------|----|------|
| **Sprint 1** | PB-01, PB-06, PB-16, PB-17, PB-18 | 31 | 124시간 |
| **Sprint 2** | PB-02, PB-03, PB-04, PB-05 | 18 | 72시간 |
| **Sprint 3** | PB-07, PB-08, PB-19, PB-20 | 26 | 104시간 |
| **Sprint 4** | PB-21, PB-22 | 8 | 32시간 |
| **총계** | **MVP 완료** | **83 SP** | **332시간** |

> **MVP 출시**: **Sprint 4 종료 후 (8주)**  
> **기능**: 자동 감지 + 로그 + 동기화 + 설정 + 백업 + 출시

---

## **리소스 할당 예시 (1인당 80시간/스프린트)**

| 역할 | Sprint 1 | Sprint 2 | Sprint 3 | Sprint 4 |
|------|----------|----------|----------|----------|
| **WatchOS** | PB-01, PB-06 | PB-02~05 | PB-07 | - |
| **iOS** | PB-16~18 | - | PB-08, PB-20 | PB-21 |
| **Backend** | - | - | PB-19 | PB-22 |
| **QA** | 테스트 | 테스트 | 테스트 | 릴리즈 검증 |

---
