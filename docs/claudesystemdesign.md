3개 레이어 간의 모듈 관계를 상세하게 그려드렸습니다. 주요 특징을 설명하겠습니다:

## 📊 시스템 모듈 구조

### ⌚ **Apple Watch Ultra 2 (검정색)**
**역할**: 실시간 센싱 & 오프라인 로깅
- **Sensor APIs**: 압력계, 심박수, 수온 센서로 0.5초 주기 데이터 수집
- **Core Modules**: 세션 자동 관리, 실시간 모니터링, 안전 알림, 회복 타이머
- **Data Layer**: 오프라인 로컬 저장 → 동기화 큐 관리

### 📱 **iPhone (파란색)**
**역할**: 데이터 분석 & 시각화 & 커뮤니티
- **Sync Manager**: Watch로부터 데이터 수신 → 로컬 저장 → iCloud 백업
- **Analytics Engine**: 세션 통계, PB 추적, 트렌드 분석
- **Visualization**: 수심-시간 그래프, 차트 생성
- **Community Manager**: 버디, 다이브 스팟, 챌린지 관리

### ☁️ **Backend (녹색)**
**역할**: 중앙 데이터 관리 & AI 분석
- **API Gateway**: 인증/인가, 라우팅, Rate Limiting
- **Microservices**: User, Dive, Social, Challenge 서비스 분리
- **AI/ML Pipeline**: 훈련 추천, 인사이트 분석
- **Data Storage**: PostgreSQL(주 DB), Redis(캐시), S3(미디어)

## 🔄 핵심 데이터 플로우

1. **Watch → iPhone**: WatchConnectivity (Bluetooth/WiFi)
2. **iPhone → Backend**: HTTPS REST API
3. **Backend → iPhone**: 푸시 알림, 실시간 업데이트
4. **Watch ↔ iPhone**: 양방향 설정 동기화

이 구조는 **오프라인 우선 설계**로 네트워크 없이도 Watch와 iPhone이 독립적으로 동작하며, Backend는 선택적 확장 기능을 제공합니다.
