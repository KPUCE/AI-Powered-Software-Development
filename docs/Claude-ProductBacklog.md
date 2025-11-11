# 🏊 FreeDivingLog Product Backlog
## Scrum Framework - Agile Development

---

## 📋 Product Backlog Overview

### Priority Levels
- 🔴 **Critical (P0)**: MVP 필수 기능
- 🟠 **High (P1)**: 핵심 기능
- 🟡 **Medium (P2)**: 중요 기능
- 🟢 **Low (P3)**: 부가 기능

### Story Points (Fibonacci)
- 1, 2, 3, 5, 8, 13, 21

### Definition of Done (DoD)
- [ ] 코드 작성 완료
- [ ] 단위 테스트 작성 및 통과
- [ ] 코드 리뷰 완료
- [ ] 통합 테스트 통과
- [ ] 문서화 완료
- [ ] QA 승인

---

## 🎯 Epic 1: 사용자 인증 및 설정 관리
**Goal**: Apple 생태계 기반 사용자 인증 및 초기 설정

### User Stories

#### US-1.1: Apple Sign-In 연동 (iPhone)
**Priority**: 🔴 P0 | **Story Points**: 5 | **Sprint**: 1
```
As a 사용자
I want to Apple ID로 로그인하고 싶다
So that 별도 회원가입 없이 빠르게 시작할 수 있다

Acceptance Criteria:
- [ ] Apple Sign-In 버튼 구현
- [ ] Apple ID 인증 성공 시 사용자 정보 저장
- [ ] 이메일, 이름 정보 수신
- [ ] JWT 토큰 발급 및 저장

Technical Notes:
- iOS: AuthenticationServices framework
- Backend: Apple Sign-In REST API 검증
```

#### US-1.2: 사용자 프로필 생성 (Backend)
**Priority**: 🔴 P0 | **Story Points**: 3 | **Sprint**: 1
```
As a 백엔드 시스템
I want to 사용자 정보를 DB에 저장하고 싶다
So that 사용자별 데이터를 관리할 수 있다

Acceptance Criteria:
- [ ] USERS 테이블 생성
- [ ] user_id(UUID) 자동 생성
- [ ] apple_id unique constraint 적용
- [ ] 기본 USER_SETTINGS 자동 생성

Technical Notes:
- PostgreSQL 트리거 사용
- Default settings: target_depth=40m, recovery=120sec
```

#### US-1.3: 초기 설정 온보딩 (iPhone)
**Priority**: 🔴 P0 | **Story Points**: 5 | **Sprint**: 1
```
As a 신규 사용자
I want to 초기 설정을 간편하게 완료하고 싶다
So that 내 프리다이빙 레벨에 맞는 경험을 할 수 있다

Acceptance Criteria:
- [ ] 자격증 레벨 선택 (Beginner/Advanced/Instructor)
- [ ] 목표 깊이 설정 (10-100m)
- [ ] 단위 시스템 선택 (Metric/Imperial)
- [ ] 언어 선택 (English/한국어)

Technical Notes:
- SwiftUI 온보딩 플로우 (4페이지)
- UserDefaults 임시 저장 후 API 전송
```

#### US-1.4: Watch-iPhone 설정 동기화
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 2
```
As a 사용자
I want to iPhone에서 변경한 설정이 Watch에 자동 반영되길 원한다
So that 매번 양쪽에서 설정할 필요가 없다

Acceptance Criteria:
- [ ] WatchConnectivity 세션 설정
- [ ] iPhone 설정 변경 시 Watch로 전송
- [ ] Watch 설정 변경 시 iPhone으로 전송
- [ ] 양방향 동기화 충돌 해결

Technical Notes:
- WatchConnectivity framework
- 최종 변경 시각 기준 충돌 해결
```

---

## 🎯 Epic 2: 실시간 다이빙 모니터링 (Apple Watch)
**Goal**: Watch에서 다이빙 중 실시간 센서 데이터 수집 및 표시

### User Stories

#### US-2.1: 센서 데이터 수집 (Watch)
**Priority**: 🔴 P0 | **Story Points**: 13 | **Sprint**: 2
```
As a Apple Watch 앱
I want to 압력 센서로 수심을 측정하고 싶다
So that 실시간 다이빙 데이터를 수집할 수 있다

Acceptance Criteria:
- [ ] CoreMotion 압력계 초기화
- [ ] 0.5초 주기 데이터 수집
- [ ] 수심 계산 (압력 → 미터)
- [ ] 메모리 버퍼에 저장 (depth_time_series)
- [ ] HealthKit 심박수 수집

Technical Notes:
- CMPressure 사용
- 압력(hPa) → 수심(m) 변환: depth = (pressure - 1013.25) / 98.0638
- 배터리 최적화: 다이빙 중에만 활성화
```

#### US-2.2: 다이브 세션 자동 감지 (Watch)
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 2
```
As a 프리다이버
I want to 수심 1m 도달 시 자동으로 다이빙이 시작되길 원한다
So that 버튼 조작 없이 다이빙에 집중할 수 있다

Acceptance Criteria:
- [ ] 수심 >= 1m, 2초 지속 시 자동 시작
- [ ] 세션 ID 생성 및 메모리 버퍼 초기화
- [ ] 수면(0m ± 0.3m) 복귀 시 자동 종료
- [ ] Dive Count 자동 증가

Technical Notes:
- 상태 머신: IDLE → DIVING → SURFACE → IDLE
- Debounce 로직으로 오탐 방지
```

#### US-2.3: 실시간 UI 업데이트 (Watch)
**Priority**: 🔴 P0 | **Story Points**: 5 | **Sprint**: 3
```
As a 다이버
I want to 현재 수심과 잠수시간을 한눈에 보고 싶다
So that 다이빙 상태를 실시간으로 파악할 수 있다

Acceptance Criteria:
- [ ] 수심 표시 (56-64px 초대형 폰트)
- [ ] 잠수시간 표시 (초 단위)
- [ ] 심박수 표시
- [ ] 수온 표시
- [ ] Always-On Display 최적화

Technical Notes:
- SwiftUI @Published 프로퍼티
- 0.5초 주기 UI 업데이트
- 고대비 색상 (검정 배경 + 흰색/형광)
```

#### US-2.4: 목표깊이 햅틱 알림 (Watch)
**Priority**: 🔴 P0 | **Story Points**: 3 | **Sprint**: 3
```
As a 다이버
I want to 목표 깊이 도달 시 진동으로 알림받고 싶다
So that 화면을 보지 않고도 목표 달성을 알 수 있다

Acceptance Criteria:
- [ ] current_depth >= target_depth 감지
- [ ] 중간 세기 진동 2회
- [ ] 초록 배경 1초 표시
- [ ] 알림 후 다이빙 모드로 복귀

Technical Notes:
- WKInterfaceDevice.hapticFeedback(.success)
- 중복 알림 방지 (플래그 사용)
```

#### US-2.5: 상승속도 경고 (Watch)
**Priority**: 🔴 P0 | **Story Points**: 5 | **Sprint**: 3
```
As a 다이버
I want to 너무 빠르게 상승할 때 경고를 받고 싶다
So that 감압병 위험을 예방할 수 있다

Acceptance Criteria:
- [ ] 상승속도 실시간 계산 (delta_depth / delta_time)
- [ ] ascent_speed > 1.2 m/s 시 경고
- [ ] 강한 진동 3회
- [ ] 빨간 배경 + "TOO FAST!" 메시지
- [ ] 속도 정상화 시 자동 복귀

Technical Notes:
- 이동 평균 필터로 노이즈 제거
- hapticFeedback(.failure) 반복
```

#### US-2.6: 수면 회복 타이머 (Watch)
**Priority**: 🟠 P1 | **Story Points**: 5 | **Sprint**: 4
```
As a 다이버
I want to 수면에 도달하면 자동으로 회복 타이머가 시작되길 원한다
So that 적절한 휴식 시간을 확보할 수 있다

Acceptance Criteria:
- [ ] 수면 도달(0m ± 0.3m) 자동 감지
- [ ] 타이머 시작 (카운트업)
- [ ] 권장 회복시간 표시 (설정값)
- [ ] 회복시간 < 설정값 시 노란 배경 경고
- [ ] 다음 다이브 시작 시 타이머 리셋

Technical Notes:
- Timer.publish(every: 1.0) 사용
- 다이브 시간:회복시간 비율 계산 (1:2 권장)
```

---

## 🎯 Epic 3: 오프라인 데이터 저장 및 동기화
**Goal**: Watch 로컬 저장 → iPhone 전송 → Backend 동기화

### User Stories

#### US-3.1: Watch 로컬 저장 (CoreData)
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 4
```
As a Apple Watch 앱
I want to 다이빙 데이터를 로컬에 저장하고 싶다
So that 네트워크 없이도 데이터를 보존할 수 있다

Acceptance Criteria:
- [ ] CoreData 모델 정의 (WatchDiveSession, WatchDiveLog)
- [ ] 다이브 종료 시 메모리 → CoreData 저장
- [ ] isSynced 플래그 관리
- [ ] 최대 1000개 세션 보관

Technical Notes:
- NSPersistentContainer 사용
- 30일 지난 동기화 완료 데이터 자동 삭제
```

#### US-3.2: Watch → iPhone 동기화
**Priority**: 🔴 P0 | **Story Points**: 13 | **Sprint**: 5
```
As a Watch 앱
I want to 다이빙 데이터를 iPhone으로 전송하고 싶다
So that 사용자가 상세 분석을 볼 수 있다

Acceptance Criteria:
- [ ] WatchConnectivity 메시지 전송
- [ ] iPhone 연결 감지 시 미동기화 데이터 전송
- [ ] 전송 성공 시 isSynced = true 업데이트
- [ ] 실패 시 재시도 큐 추가 (최대 5회)
- [ ] 10초 이내 전송 완료

Technical Notes:
- WCSession.transferUserInfo() 사용
- 백그라운드 15분마다 재시도
```

#### US-3.3: iPhone 로컬 저장
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 5
```
As a iPhone 앱
I want to Watch로부터 받은 데이터를 저장하고 싶다
So that 전체 다이빙 히스토리를 관리할 수 있다

Acceptance Criteria:
- [ ] CoreData 모델 정의 (DiveSession, DiveLog)
- [ ] Watch 데이터 수신 시 파싱 및 저장
- [ ] 중복 데이터 방지 (session_id 기준)
- [ ] NSFetchedResultsController로 UI 자동 업데이트

Technical Notes:
- CoreData + CloudKit 연동
- 인덱싱: session_date, user_id
```

#### US-3.4: iCloud 자동 백업
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 6
```
As a 사용자
I want to 내 데이터가 iCloud에 자동 백업되길 원한다
So that 기기를 바꿔도 데이터가 보존된다

Acceptance Criteria:
- [ ] CloudKit Container 설정
- [ ] CoreData + CloudKit 동기화
- [ ] 자동 백업 활성화
- [ ] 복원 기능 구현

Technical Notes:
- NSPersistentCloudKitContainer 사용
- Public/Private Database 구분
```

#### US-3.5: iPhone → Backend 동기화
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 6
```
As a iPhone 앱
I want to 로컬 데이터를 서버로 전송하고 싶다
So that 다른 플랫폼(웹)에서도 접근할 수 있다

Acceptance Criteria:
- [ ] REST API 엔드포인트 연동
- [ ] JWT 토큰 인증
- [ ] 미동기화 데이터 배치 전송
- [ ] 네트워크 실패 시 재시도
- [ ] 동기화 성공률 99% 달성

Technical Notes:
- Alamofire 또는 URLSession
- Exponential backoff 재시도 전략
```

---

## 🎯 Epic 4: iPhone 데이터 시각화 및 분석
**Goal**: 다이빙 로그를 그래프와 통계로 시각화

### User Stories

#### US-4.1: Dashboard 화면 (iPhone)
**Priority**: 🔴 P0 | **Story Points**: 13 | **Sprint**: 7
```
As a 사용자
I want to 대시보드에서 나의 프리다이빙 현황을 한눈에 보고 싶다
So that 빠르게 내 상태를 파악할 수 있다

Acceptance Criteria:
- [ ] Personal Best 카드 (최대 수심, 최대 시간)
- [ ] Quick Stats (주간 다이브 수, 평균 수심, 평균 시간, 연속 일수)
- [ ] 진행률 차트 (월간 Depth Trend)
- [ ] AI Insights 카드
- [ ] 최근 활동 피드

Technical Notes:
- SwiftUI + Combine
- Charts framework (iOS 16+)
```

#### US-4.2: 세션 목록 화면 (iPhone)
**Priority**: 🔴 P0 | **Story Points**: 5 | **Sprint**: 7
```
As a 사용자
I want to 내 모든 다이빙 세션을 날짜별로 보고 싶다
So that 과거 기록을 쉽게 찾을 수 있다

Acceptance Criteria:
- [ ] 세션 카드 목록 (날짜, 다이브 수, 최대 수심, 총 시간)
- [ ] PB 배지 표시
- [ ] 무한 스크롤
- [ ] 날짜별 정렬 (최신순)

Technical Notes:
- LazyVStack + NSFetchedResultsController
- Pagination (20개씩)
```

#### US-4.3: 수심-시간 그래프 (iPhone)
**Priority**: 🔴 P0 | **Story Points**: 13 | **Sprint**: 8
```
As a 사용자
I want to 다이브별 수심-시간 프로파일을 그래프로 보고 싶다
So that 내 다이빙 패턴을 분석할 수 있다

Acceptance Criteria:
- [ ] depth_time_series JSONB 파싱
- [ ] Line Chart 렌더링
- [ ] X축: 시간(초), Y축: 수심(m)
- [ ] 터치로 특정 시점 상세 정보 표시
- [ ] 다이브별 색상 구분

Technical Notes:
- Charts framework
- JSONB → [CGPoint] 변환
```

#### US-4.4: 세션 상세 화면 (iPhone)
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 8
```
As a 사용자
I want to 세션 내 모든 다이브의 상세 정보를 보고 싶다
So that 각 다이브를 비교 분석할 수 있다

Acceptance Criteria:
- [ ] 세션 전체 그래프 (모든 다이브 overlay)
- [ ] 개별 다이브 목록 (수심, 시간, 회복시간)
- [ ] 회복시간 경고 표시 (⚠️)
- [ ] PB 다이브 하이라이트 (🏆)

Technical Notes:
- NavigationLink 전환
- 다이브별 컬러 코딩
```

#### US-4.5: 통계 화면 (iPhone)
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 9
```
As a 사용자
I want to 주간/월간/연간 통계를 보고 싶다
So that 장기적인 진행 상황을 추적할 수 있다

Acceptance Criteria:
- [ ] 기간 필터 (Week/Month/Year)
- [ ] Bar Chart (주별 다이브 수)
- [ ] 평균 수심 진행률
- [ ] 평균 시간 진행률
- [ ] 회복 비율 점수
- [ ] 전월 대비 증감률 표시

Technical Notes:
- PostgreSQL 집계 쿼리
- Backend API: /api/stats?period=month
```

#### US-4.6: PDF/CSV 내보내기 (iPhone)
**Priority**: 🟡 P2 | **Story Points**: 8 | **Sprint**: 10
```
As a 사용자
I want to 내 다이빙 기록을 PDF나 CSV로 내보내고 싶다
So that 코치와 공유하거나 인쇄할 수 있다

Acceptance Criteria:
- [ ] 세션별 PDF 생성 (그래프 포함)
- [ ] 전체 로그 CSV 내보내기
- [ ] 공유 시트 (AirDrop, 메일 등)

Technical Notes:
- PDFKit for PDF generation
- CSV: URLSession downloadTask
```

---

## 🎯 Epic 5: Backend API 개발
**Goal**: RESTful API로 데이터 CRUD 및 비즈니스 로직 처리

### User Stories

#### US-5.1: 인증 API
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 1
```
As a Backend 시스템
I want to Apple Sign-In 토큰을 검증하고 JWT를 발급하고 싶다
So that 안전한 사용자 인증을 제공할 수 있다

Acceptance Criteria:
- [ ] POST /api/auth/apple
- [ ] Apple identity token 검증
- [ ] JWT 토큰 생성 (유효기간 30일)
- [ ] Refresh token 발급

Technical Notes:
- Node.js + Express or FastAPI
- jsonwebtoken 라이브러리
```

#### US-5.2: 다이빙 로그 API
**Priority**: 🔴 P0 | **Story Points**: 13 | **Sprint**: 6
```
As a iPhone 앱
I want to 다이빙 로그를 서버에 저장하고 조회하고 싶다
So that 멀티 플랫폼에서 데이터를 공유할 수 있다

Acceptance Criteria:
- [ ] POST /api/sessions (세션 생성)
- [ ] POST /api/sessions/:id/dives (다이브 추가)
- [ ] GET /api/sessions (세션 목록)
- [ ] GET /api/sessions/:id (세션 상세)
- [ ] PUT /api/sessions/:id (세션 수정)
- [ ] DELETE /api/sessions/:id (세션 삭제)

Technical Notes:
- RESTful 설계
- Pagination (limit, offset)
- JWT 인증 미들웨어
```

#### US-5.3: 통계 API
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 9
```
As a iPhone 앱
I want to 사용자 통계를 서버에서 계산받고 싶다
So that 클라이언트 부하를 줄일 수 있다

Acceptance Criteria:
- [ ] GET /api/stats/summary (전체 요약)
- [ ] GET /api/stats/progress?period=month (진행률)
- [ ] GET /api/stats/personal-bests (PB 목록)
- [ ] POST /api/stats/calculate (세션 통계 재계산)

Technical Notes:
- PostgreSQL Window Functions
- Redis 캐싱 (1시간)
```

#### US-5.4: 다이브 스팟 API
**Priority**: 🟡 P2 | **Story Points**: 13 | **Sprint**: 11
```
As a iPhone 앱
I want to 다이브 스팟 정보를 조회하고 리뷰를 작성하고 싶다
So that 커뮤니티 정보를 공유할 수 있다

Acceptance Criteria:
- [ ] GET /api/spots (스팟 목록)
- [ ] GET /api/spots/nearby?lat=&lng= (주변 스팟)
- [ ] POST /api/spots (스팟 생성)
- [ ] POST /api/spots/:id/reviews (리뷰 작성)
- [ ] GET /api/spots/:id/reviews (리뷰 목록)

Technical Notes:
- PostGIS spatial queries
- Haversine formula for distance
```

---

## 🎯 Epic 6: AI 기능 및 분석
**Goal**: 머신러닝 기반 훈련 추천 및 인사이트

### User Stories

#### US-6.1: SESSION_STATS 자동 계산
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 9
```
As a Backend 시스템
I want to 세션 종료 시 통계를 자동 계산하고 싶다
So that 사용자에게 즉시 분석 결과를 제공할 수 있다

Acceptance Criteria:
- [ ] efficiency_score 계산 (0-100)
- [ ] safety_score 계산 (회복시간 기준)
- [ ] depth_distribution 히스토그램 생성
- [ ] recovery_ratio 계산

Technical Notes:
- PostgreSQL Trigger or Backend Job
- 계산 로직: efficiency = (avg_depth / max_possible) * 100
```

#### US-6.2: AI 훈련 추천 엔진
**Priority**: 🟡 P2 | **Story Points**: 21 | **Sprint**: 12
```
As a 사용자
I want to AI가 내 데이터를 분석해 훈련 계획을 추천받고 싶다
So that 더 효과적으로 실력을 향상시킬 수 있다

Acceptance Criteria:
- [ ] 최근 30일 데이터 분석
- [ ] 진행 패턴 인식 (상승/정체/하락)
- [ ] 개인화된 훈련 계획 생성
- [ ] confidence_score 제공

Technical Notes:
- Python + scikit-learn
- Linear Regression for trend analysis
- 주 1회 배치 실행
```

#### US-6.3: Personal Best 자동 감지
**Priority**: 🟠 P1 | **Story Points**: 5 | **Sprint**: 10
```
As a 시스템
I want to 새로운 PB 달성 시 자동으로 기록하고 싶다
So that 사용자에게 축하 메시지를 보낼 수 있다

Acceptance Criteria:
- [ ] 다이브 종료 시 PB 체크
- [ ] MAX_DEPTH, MAX_TIME, MAX_STREAK 비교
- [ ] PERSONAL_BESTS 테이블 업데이트
- [ ] 푸시 알림 전송

Technical Notes:
- PostgreSQL Trigger
- APNS (Apple Push Notification Service)
```

---

## 🎯 Epic 7: 커뮤니티 기능
**Goal**: 버디 시스템 및 다이브 스팟 공유

### User Stories

#### US-7.1: 버디 추가 (iPhone)
**Priority**: 🟡 P2 | **Story Points**: 8 | **Sprint**: 13
```
As a 사용자
I want to 다른 다이버를 버디로 추가하고 싶다
So that 함께 다이빙한 기록을 공유할 수 있다

Acceptance Criteria:
- [ ] 사용자 검색 (이름, 이메일)
- [ ] 버디 요청 전송
- [ ] 요청 수락/거절
- [ ] 버디 목록 표시

Technical Notes:
- POST /api/buddies/request
- BUDDIES 테이블 status 관리
```

#### US-7.2: 다이브 스팟 지도 (iPhone)
**Priority**: 🟡 P2 | **Story Points**: 13 | **Sprint**: 11
```
As a 사용자
I want to 지도에서 주변 다이브 스팟을 보고 싶다
So that 새로운 장소를 발견할 수 있다

Acceptance Criteria:
- [ ] MapKit 연동
- [ ] 현재 위치 표시
- [ ] 스팟 마커 표시
- [ ] 마커 탭 시 스팟 정보 표시
- [ ] 거리순 정렬

Technical Notes:
- MapKit + SwiftUI
- MKAnnotation 커스텀
```

#### US-7.3: 챌린지 시스템 (iPhone)
**Priority**: 🟢 P3 | **Story Points**: 21 | **Sprint**: 14
```
As a 사용자
I want to 챌린지에 참여하고 순위를 확인하고 싶다
So that 동기부여를 받을 수 있다

Acceptance Criteria:
- [ ] 활성 챌린지 목록
- [ ] 챌린지 가입
- [ ] 진행률 표시
- [ ] 리더보드 (순위)

Technical Notes:
- Redis Sorted Set for 실시간 랭킹
- 주간/월간 챌린지
```

---

## 🎯 Epic 8: 설정 및 사용자 경험
**Goal**: 사용자 맞춤 설정 및 다국어 지원

### User Stories

#### US-8.1: 단위 시스템 전환
**Priority**: 🟠 P1 | **Story Points**: 5 | **Sprint**: 2
```
As a 사용자
I want to 미터/피트, 섭씨/화씨를 선택하고 싶다
So that 내가 익숙한 단위로 볼 수 있다

Acceptance Criteria:
- [ ] 설정 화면에서 단위 선택
- [ ] 모든 화면 실시간 변환
- [ ] 1m = 3.28084ft 정확도
- [ ] °F = (°C × 9/5) + 32

Technical Notes:
- Formatter 클래스 구현
- UserDefaults 저장
```

#### US-8.2: 다국어 지원 (i18n)
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 2
```
As a 사용자
I want to 영어/한국어로 앱을 사용하고 싶다
So that 내 모국어로 편하게 사용할 수 있다

Acceptance Criteria:
- [ ] Localizable.strings 파일 생성 (en, ko)
- [ ] 모든 UI 텍스트 번역
- [ ] 언어 변경 시 앱 재시작 없이 적용
- [ ] Watch와 iPhone 언어 동기화

Technical Notes:
- NSLocalizedString() 사용
- 200+ 문자열 번역 필요
```

#### US-8.3: 알림 설정 (iPhone)
**Priority**: 🟡 P2 | **Story Points**: 5 | **Sprint**: 10
```
As a 사용자
I want to 알림을 커스터마이즈하고 싶다
So that 내 스타일에 맞게 조정할 수 있다

Acceptance Criteria:
- [ ] 푸시 알림 ON/OFF
- [ ] 햅틱 피드백 강도 조절
- [ ] 알림 유형별 설정 (PB, 경고, 챌린지)
- [ ] 방해금지 시간 설정

Technical Notes:
- UNUserNotificationCenter
- USER_SETTINGS.notification_preferences JSONB
```

#### US-8.4: 데이터 내보내기 (iPhone)
**Priority**: 🟡 P2 | **Story Points**: 8 | **Sprint**: 10
```
As a 사용자
I want to 내 모든 데이터를 백업하고 싶다
So that 데이터 손실을 방지할 수 있다

Acceptance Criteria:
- [ ] 전체 데이터 JSON 내보내기
- [ ] CSV 내보내기 (Excel 호환)
- [ ] PDF 리포트 생성
- [ ] 이메일/AirDrop 공유

Technical Notes:
- Codable protocol
- CSVExporter 유틸리티
```

---

## 🎯 Epic 9: 성능 최적화 및 안정성
**Goal**: 배터리 효율, 속도, 안정성 향상

### User Stories

#### US-9.1: Watch 배터리 최적화
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 4
```
As a Apple Watch 앱
I want to 배터리 소모를 최소화하고 싶다
So that 2시간 다이빙 중 15% 미만 소모를 달성할 수 있다

Acceptance Criteria:
- [ ] 다이빙 중에만 센서 활성화
- [ ] Always-On Display 밝기 최적화
- [ ] 백그라운드 작업 최소화
- [ ] 실제 테스트: 2시간 < 15% 소모

Technical Notes:
- Instruments로 프로파일링
- WKExtension.shared.isApplicationActive 체크
```

#### US-9.2: 오프라인 모드 안정성
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 5
```
As a Watch/iPhone 앱
I want to 네트워크 없이도 완벽히 동작하고 싶다
So that 수중에서도 데이터 손실이 없다

Acceptance Criteria:
- [ ] 모든 기능 오프라인 동작
- [ ] 동기화 큐 관리
- [ ] 네트워크 복구 시 자동 재시도
- [ ] 데이터 무결성 보장

Technical Notes:
- Network reachability 모니터링
- CoreData persistent store
```

#### US-9.3: 동기화 성공률 99% 달성
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 6
```
As a 시스템
I want to 동기화 성공률을 99% 이상 유지하고 싶다
So that 사용자 데이터가 손실되지 않는다

Acceptance Criteria:
- [ ] 재시도 메커니즘 (Exponential backoff)
- [ ] 동기화 실패 로깅
- [ ] 모니터링 대시보드
- [ ] 성공률 99% 이상 달성

Technical Notes:
- SYNC_LOGS 테이블 분석
- Prometheus + Grafana 모니터링
```

#### US-9.4: DB 쿼리 최적화
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 9
```
As a Backend 시스템
I want to 모든 API가 200ms 이내 응답하길 원한다
So that 사용자 경험이 빠르다

Acceptance Criteria:
- [ ] 주요 쿼리 인덱싱
- [ ] N+1 쿼리 제거
- [ ] Redis 캐싱 적용
- [ ] 평균 응답시간 < 200ms

Technical Notes:
- EXPLAIN ANALYZE로 쿼리 분석
- Connection pooling (PgBouncer)
```

---

## 🎯 Epic 10: 테스트 및 품질 보증
**Goal**: 자동화 테스트 및 QA 프로세스 구축

### User Stories

#### US-10.1: Watch 유닛 테스트
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 3-4
```
As a 개발팀
I want to Watch 앱 핵심 로직을 테스트하고 싶다
So that 버그를 조기에 발견할 수 있다

Acceptance Criteria:
- [ ] 센서 데이터 처리 테스트
- [ ] 상태 머신 테스트 (IDLE → DIVING → SURFACE)
- [ ] 알림 트리거 테스트
- [ ] 코드 커버리지 > 80%

Technical Notes:
- XCTest framework
- Mock CoreMotion data
```

#### US-10.2: iPhone 유닛 테스트
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 7-8
```
As a 개발팀
I want to iPhone 앱 비즈니스 로직을 테스트하고 싶다
So that 안정적인 앱을 배포할 수 있다

Acceptance Criteria:
- [ ] ViewModel 테스트
- [ ] API 통신 테스트 (Mock)
- [ ] CoreData 로직 테스트
- [ ] 코드 커버리지 > 80%

Technical Notes:
- XCTest + Combine testing
- MockURLProtocol for API mocking
```

#### US-10.3: Backend API 테스트
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 6
```
As a 개발팀
I want to 모든 API 엔드포인트를 테스트하고 싶다
So that API 안정성을 보장할 수 있다

Acceptance Criteria:
- [ ] 단위 테스트 (각 엔드포인트)
- [ ] 통합 테스트 (DB 연동)
- [ ] 부하 테스트 (1000 req/sec)
- [ ] 코드 커버리지 > 85%

Technical Notes:
- Jest (Node.js) or Pytest (Python)
- Locust for load testing
```

#### US-10.4: E2E 시나리오 테스트
**Priority**: 🟡 P2 | **Story Points**: 21 | **Sprint**: 11
```
As a QA팀
I want to 전체 사용자 플로우를 자동 테스트하고 싶다
So that 릴리즈 전 버그를 발견할 수 있다

Acceptance Criteria:
- [ ] Watch 다이빙 시나리오
- [ ] iPhone 데이터 확인 시나리오
- [ ] 동기화 시나리오
- [ ] 10개 주요 시나리오 자동화

Technical Notes:
- XCUITest for UI testing
- CI/CD 파이프라인 통합
```

---

## 🎯 Epic 11: 배포 및 운영
**Goal**: 프로덕션 배포 및 모니터링 시스템 구축

### User Stories

#### US-11.1: CI/CD 파이프라인 구축
**Priority**: 🟠 P1 | **Story Points**: 13 | **Sprint**: 5
```
As a DevOps팀
I want to 자동 빌드 및 배포 파이프라인을 구축하고 싶다
So that 빠르고 안정적으로 배포할 수 있다

Acceptance Criteria:
- [ ] GitHub Actions 워크플로우
- [ ] 자동 테스트 실행
- [ ] TestFlight 자동 배포
- [ ] 배포 실패 시 롤백

Technical Notes:
- Fastlane for iOS deployment
- Docker for backend
```

#### US-11.2: 모니터링 시스템
**Priority**: 🟠 P1 | **Story Points**: 8 | **Sprint**: 9
```
As a 운영팀
I want to 실시간 시스템 상태를 모니터링하고 싶다
So that 장애를 빠르게 대응할 수 있다

Acceptance Criteria:
- [ ] API 응답시간 모니터링
- [ ] 에러율 추적
- [ ] 동기화 성공률 추적
- [ ] 알림 설정 (Slack)

Technical Notes:
- Prometheus + Grafana
- Sentry for error tracking
```

#### US-11.3: App Store 출시
**Priority**: 🔴 P0 | **Story Points**: 8 | **Sprint**: 15
```
As a 프로덕트팀
I want to App Store에 앱을 출시하고 싶다
So that 사용자가 다운로드할 수 있다

Acceptance Criteria:
- [ ] App Store Connect 설정
- [ ] 스크린샷 및 설명 준비
- [ ] 개인정보 보호정책 작성
- [ ] Apple 심사 통과

Technical Notes:
- App Store Guidelines 준수
- Privacy Manifest 포함
```

---

## 📊 Sprint Planning 예시

### **Sprint 1 (2 weeks)** - MVP Foundation
**Goal**: 사용자 인증 및 기본 설정
- US-1.1: Apple Sign-In (5pt)
- US-1.2: 사용자 프로필 생성 (3pt)
- US-1.3: 초기 설정 온보딩 (5pt)
- US-5.1: 인증 API (8pt)
- **Total**: 21pt

### **Sprint 2 (2 weeks)** - Watch 센서 수집
**Goal**: 실시간 다이빙 데이터 수집
- US-1.4: Watch-iPhone 설정 동기화 (8pt)
- US-2.1: 센서 데이터 수집 (13pt)
- US-2.2: 다이브 세션 자동 감지 (8pt)
- US-8.1: 단위 시스템 전환 (5pt)
- US-8.2: 다국어 지원 (8pt)
- **Total**: 42pt (2팀 병렬)

### **Sprint 3 (2 weeks)** - Watch UI & 알림
**Goal**: 사용자 피드백 시스템
- US-2.3: 실시간 UI 업데이트 (5pt)
- US-2.4: 목표깊이 햅틱 알림 (3pt)
- US-2.5: 상승속도 경고 (5pt)
- US-10.1: Watch 유닛 테스트 (13pt)
- **Total**: 26pt

### **Sprint 4 (2 weeks)** - 데이터 저장
**Goal**: 오프라인 데이터 관리
- US-2.6: 수면 회복 타이머 (5pt)
- US-3.1: Watch 로컬 저장 (8pt)
- US-9.1: Watch 배터리 최적화 (8pt)
- **Total**: 21pt

### **Sprint 5 (2 weeks)** - 동기화
**Goal**: Watch ↔ iPhone ↔ Backend 연결
- US-3.2: Watch → iPhone 동기화 (13pt)
- US-3.3: iPhone 로컬 저장 (8pt)
- US-9.2: 오프라인 모드 안정성 (8pt)
- US-11.1: CI/CD 파이프라인 (13pt)
- **Total**: 42pt (2팀 병렬)

### **Sprint 6 (2 weeks)** - Backend 연동
**Goal**: 서버 데이터 동기화
- US-3.4: iCloud 자동 백업 (8pt)
- US-3.5: iPhone → Backend 동기화 (13pt)
- US-5.2: 다이빙 로그 API (13pt)
- US-9.3: 동기화 성공률 99% (13pt)
- US-10.3: Backend API 테스트 (13pt)
- **Total**: 60pt (3팀 병렬)

### **Sprint 7-15**: 계속...

---

## 📈 Release Plan

### **Release 1.0 (MVP)** - Sprint 1-10 (20주)
**기능**:
- ✅ Apple Sign-In 인증
- ✅ Watch 실시간 다이빙 모니터링
- ✅ 안전 알림 (목표깊이, 상승속도, 회복시간)
- ✅ 오프라인 데이터 저장 및 동기화
- ✅ iPhone Dashboard & 로그 목록
- ✅ 수심-시간 그래프
- ✅ 기본 통계 (PB, 평균)
- ✅ 설정 (단위, 언어, 알림)

### **Release 1.1** - Sprint 11-13 (6주)
**기능**:
- ✅ 다이브 스팟 지도
- ✅ 스팟 리뷰 시스템
- ✅ 버디 추가
- ✅ PDF/CSV 내보내기

### **Release 1.2** - Sprint 14-15 (4주)
**기능**:
- ✅ AI 훈련 추천
- ✅ 챌린지 시스템
- ✅ 고급 통계 분석

---

## 🔥 Critical Path (MVP 최소 기능)

### Must Have (P0)
1. Apple Sign-In 인증
2. Watch 센서 데이터 수집
3. 다이브 자동 감지
4. 실시간 UI 표시
5. 안전 알림 (상승속도, 목표깊이)
6. 로컬 데이터 저장
7. Watch ↔ iPhone 동기화
8. iPhone Dashboard
9. 수심-시간 그래프
10. 기본 설정

### Should Have (P1)
- iCloud 백업
- 회복 타이머
- 통계 화면
- 단위/언어 설정
- Backend API 연동

### Could Have (P2)
- 다이브 스팟
- AI 추천
- PDF 내보내기

### Won't Have (P3)
- 챌린지 시스템 (v1.2)
- 소셜 공유 (v1.2)

---

## 📝 Notes

### Team Structure (권장)
- **Watch Team** (2명): watchOS 개발
- **iPhone Team** (2명): iOS 개발  
- **Backend Team** (2명): API 및 DB
- **QA** (1명): 테스트 자동화
- **DevOps** (1명): 인프라 및 배포

### Sprint Velocity
- **예상 Velocity**: 20-25 story points/sprint/팀
- **Sprint 기간**: 2주
- **MVP 기간**: 10 sprints (20주, ~5개월)

### Definition of Ready (DoR)
- [ ] User Story 명확히 정의됨
- [ ] Acceptance Criteria 작성됨
- [ ] 기술적 제약사항 파악됨
- [ ] UI/UX 디자인 준비됨
- [ ] 의존성 해결됨

### Risks & Mitigation
| Risk | 확률 | 영향 | Mitigation |
|------|------|------|------------|
| Apple Watch 센서 정확도 이슈 | 중 | 높음 | 실제 다이빙 테스트 반복 |
| 배터리 소모 초과 | 중 | 높음 | 조기 프로파일링 및 최적화 |
| 동기화 실패 | 낮 | 중 | 재시도 로직 강화 |
| App Store 심사 거부 | 낮 | 높음 | 가이드라인 사전 검토 |

---

## 🎯 Success Metrics (KPI)

### Technical Metrics
- ✅ 동기화 성공률 ≥ 99%
- ✅ API 응답시간 < 200ms
- ✅ Watch 배터리 소모 < 15% (2시간)
- ✅ 앱 크래시율 < 0.1%
- ✅ 코드 커버리지 > 80%

### Business Metrics (1년 내)
- ✅ 다운로드 수 ≥ 10,000
- ✅ MAU ≥ 3,000 (30% DAU)
- ✅ 평균 세션 로그 ≥ 8회/주
- ✅ App Store 평점 ≥ 4.5
- ✅ 사용자 리텐션 ≥ 60% (30일)

---

**Total Product Backlog Items**: 50+ User Stories
**Estimated Duration**: 15 Sprints (30 weeks, ~7.5 months)
**Team Size**: 8 members
**Total Story Points**: ~500 points
