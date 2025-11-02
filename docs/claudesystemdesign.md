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

'''mermaid

graph TB
    subgraph WATCH["⌚ Apple Watch Ultra 2 - watchOS"]
        subgraph W_UI["Presentation Layer"]
            W_HOME[Home Screen<br/>환경설정, PB 표시]
            W_DIVE[Dive Screen<br/>실시간 수심/시간/수온]
            W_SURF[Surface Screen<br/>회복타이머, 세션통계]
        end
        
        subgraph W_CORE["Core Modules"]
            W_SESSION[Session Manager<br/>· 자동 시작/종료<br/>· Dive Count 관리<br/>· 세션 상태 추적]
            W_MONITOR[Real-time Monitor<br/>· 수심 측정 0.5초 주기<br/>· 잠수시간 추적<br/>· 수온 모니터링]
            W_ALERT[Alert Manager<br/>· 목표깊이 햅틱<br/>· 상승속도 경고<br/>· 회복시간 알림]
            W_RECOVERY[Recovery Timer<br/>· 수면 복귀 감지<br/>· 휴식시간 측정<br/>· 다음 다이브 체크]
        end
        
        subgraph W_DATA["Data Layer"]
            W_STORE[Local Storage<br/>CoreData<br/>· 오프라인 캐싱<br/>· 세션 로그 저장]
            W_SYNC[Sync Queue<br/>· 동기화 대기열<br/>· 재시도 로직]
        end
        
        subgraph W_SENSOR["Sensor APIs"]
            W_DEPTH[Depth Sensor<br/>CoreMotion<br/>압력계]
            W_HR[Heart Rate<br/>HealthKit]
            W_TEMP[Temperature<br/>Sensor]
        end
    end
    
    subgraph PHONE["📱 iPhone - iOS"]
        subgraph P_UI["Presentation Layer"]
            P_LOG[Log View<br/>다이브 기록 목록]
            P_DETAIL[Detail View<br/>수심-시간 그래프]
            P_STATS[Statistics View<br/>세션별 통계]
            P_COMM[Community View<br/>버디, 스팟, 챌린지]
            P_SET[Settings View<br/>알림/장비 설정]
        end
        
        subgraph P_CORE["Core Modules"]
            P_SYNC[Sync Manager<br/>· Watch 데이터 수신<br/>· 로컬 저장 조정<br/>· 클라우드 동기화]
            P_ANALYTICS[Analytics Engine<br/>· 세션 통계 계산<br/>· PB 추적<br/>· 트렌드 분석]
            P_VIS[Visualization Engine<br/>· 수심-시간 그래프<br/>· 차트 생성<br/>· 데이터 시각화]
            P_COMMUNITY[Community Manager<br/>· 버디 관리<br/>· 스팟 지도<br/>· 챌린지/랭킹]
            P_EXPORT[Export Service<br/>· PDF 생성<br/>· CSV 내보내기<br/>· 데이터 공유]
        end
        
        subgraph P_DATA["Data Layer"]
            P_STORE[Local Database<br/>CoreData<br/>· 전체 로그 저장<br/>· 인덱싱]
            P_CLOUD[iCloud Sync<br/>CloudKit<br/>· 자동 백업<br/>· 기기간 동기화]
            P_CACHE[Cache Manager<br/>· 이미지 캐싱<br/>· API 응답 캐싱]
        end
    end
    
    subgraph BACKEND["☁️ Backend Services"]
        subgraph B_API["API Gateway Layer"]
            B_GATE[API Gateway<br/>· 인증/인가<br/>· 라우팅<br/>· Rate Limiting]
        end
        
        subgraph B_SERVICES["Microservices"]
            B_USER[User Service<br/>· 사용자 프로필<br/>· 인증 관리<br/>· 설정 동기화]
            B_DIVE[Dive Service<br/>· 로그 저장/조회<br/>· 데이터 검증<br/>· 통계 집계]
            B_SOCIAL[Social Service<br/>· 버디 시스템<br/>· 다이브 스팟<br/>· 댓글/리뷰]
            B_CHALLENGE[Challenge Service<br/>· 챌린지 관리<br/>· 랭킹 시스템<br/>· 보상 처리]
        end
        
        subgraph B_AI["AI/ML Pipeline"]
            B_RECOMMEND[Training AI<br/>· 훈련 추천<br/>· 패턴 분석<br/>· 개인화 코칭]
            B_INSIGHT[Insight Engine<br/>· 트렌드 분석<br/>· 효율성 점수<br/>· 안전 분석]
        end
        
        subgraph B_DATA["Data Storage"]
            B_DB[(Primary DB<br/>PostgreSQL<br/>· 사용자 데이터<br/>· 다이브 로그)]
            B_REDIS[(Redis Cache<br/>· 세션 캐시<br/>· 랭킹 캐시)]
            B_S3[(Object Storage<br/>S3<br/>· 이미지/동영상)]
        end
        
        subgraph B_EXT["External Services"]
            B_PUSH[Push Service<br/>APNS<br/>· 알림 전송]
            B_MAP[Map Service<br/>MapKit API<br/>· 위치 데이터]
        end
    end
    
    %% Watch Internal Flow
    W_DEPTH -->|압력 데이터| W_MONITOR
    W_HR -->|심박수| W_MONITOR
    W_TEMP -->|수온| W_MONITOR
    
    W_MONITOR -->|실시간 업데이트| W_DIVE
    W_MONITOR -->|세션 데이터| W_SESSION
    W_MONITOR -->|알림 트리거| W_ALERT
    
    W_SESSION -->|상태 변경| W_HOME
    W_SESSION -->|로그 저장| W_STORE
    W_SESSION -->|수면 감지| W_RECOVERY
    
    W_RECOVERY -->|타이머 업데이트| W_SURF
    W_ALERT -->|햅틱 피드백| W_DIVE
    
    W_STORE -->|동기화 큐| W_SYNC
    
    %% Watch to iPhone Communication
    W_SYNC ==>|WatchConnectivity<br/>Bluetooth/WiFi| P_SYNC
    
    %% iPhone Internal Flow
    P_SYNC -->|데이터 수신| P_STORE
    P_SYNC -->|백업| P_CLOUD
    
    P_STORE -->|로그 조회| P_ANALYTICS
    P_ANALYTICS -->|통계 계산| P_VIS
    P_VIS -->|그래프| P_DETAIL
    
    P_STORE -->|데이터| P_LOG
    P_ANALYTICS -->|통계| P_STATS
    
    P_STORE -->|내보내기| P_EXPORT
    P_COMMUNITY -->|소셜 데이터| P_COMM
    
    P_SET -->|설정 변경| P_SYNC
    P_SYNC -.->|설정 동기화| W_SESSION
    
    %% iPhone to Backend Communication
    P_SYNC ==>|HTTPS/REST API| B_GATE
    P_COMMUNITY ==>|API 요청| B_GATE
    
    B_GATE -->|인증| B_USER
    B_GATE -->|로그 동기화| B_DIVE
    B_GATE -->|소셜 기능| B_SOCIAL
    B_GATE -->|챌린지| B_CHALLENGE
    
    %% Backend Internal Flow
    B_USER -->|CRUD| B_DB
    B_DIVE -->|저장/조회| B_DB
    B_SOCIAL -->|데이터 저장| B_DB
    B_CHALLENGE -->|랭킹 관리| B_DB
    
    B_DIVE -->|캐싱| B_REDIS
    B_CHALLENGE -->|랭킹 캐시| B_REDIS
    B_SOCIAL -->|미디어 저장| B_S3
    
    B_DIVE -->|훈련 데이터| B_RECOMMEND
    B_DIVE -->|분석 데이터| B_INSIGHT
    
    B_RECOMMEND -->|추천 결과| B_GATE
    B_INSIGHT -->|인사이트| B_GATE
    
    B_USER -->|알림 요청| B_PUSH
    B_SOCIAL -->|위치 조회| B_MAP
    
    B_PUSH -.->|푸시 알림| P_UI
    
    %% Styling
    classDef watchStyle fill:#000000,stroke:#FF6B35,stroke-width:3px,color:#fff
    classDef phoneStyle fill:#007AFF,stroke:#0051D5,stroke-width:3px,color:#fff
    classDef backendStyle fill:#34C759,stroke:#248A3D,stroke-width:3px,color:#fff
    classDef dataStyle fill:#FF9500,stroke:#C93400,stroke-width:2px,color:#fff
    classDef aiStyle fill:#AF52DE,stroke:#8E44AD,stroke-width:2px,color:#fff
    
    class W_HOME,W_DIVE,W_SURF,W_SESSION,W_MONITOR,W_ALERT,W_RECOVERY,W_STORE,W_SYNC,W_DEPTH,W_HR,W_TEMP watchStyle
    class P_LOG,P_DETAIL,P_STATS,P_COMM,P_SET,P_SYNC,P_ANALYTICS,P_VIS,P_COMMUNITY,P_EXPORT,P_STORE,P_CLOUD,P_CACHE phoneStyle
    class B_GATE,B_USER,B_DIVE,B_SOCIAL,B_CHALLENGE,B_PUSH,B_MAP backendStyle
    class B_DB,B_REDIS,B_S3 dataStyle
    class B_RECOMMEND,B_INSIGHT aiStyle
