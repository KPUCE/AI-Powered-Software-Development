## 시스템 설계

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

```mermaid

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

## UI 설계
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreeDivingLog - Apple Watch Ultra 2 UI Mockup</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            padding: 40px 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        h1 {
            text-align: center;
            color: #ffffff;
            font-size: 32px;
            margin-bottom: 40px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
        }

        .screens-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }

        .watch-frame {
            background: linear-gradient(145deg, #2d2d2d, #1a1a1a);
            border-radius: 60px;
            padding: 20px;
            box-shadow: 
                0 20px 60px rgba(0, 0, 0, 0.6),
                inset 0 1px 2px rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .watch-frame::before {
            content: '';
            position: absolute;
            top: 50%;
            right: -8px;
            transform: translateY(-50%);
            width: 8px;
            height: 50px;
            background: linear-gradient(90deg, #3a3a3a, #2a2a2a);
            border-radius: 0 4px 4px 0;
        }

        .screen-label {
            text-align: center;
            color: #888;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 12px;
        }

        .watch-screen {
            background: #000000;
            border-radius: 45px;
            width: 100%;
            aspect-ratio: 1;
            padding: 24px;
            display: flex;
            flex-direction: column;
            color: white;
            position: relative;
            overflow: hidden;
            font-size: 14px;
        }

        .screen-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 16px;
            font-size: 13px;
            font-weight: 600;
            color: #888;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .status-dot.green { background: #00ff88; }
        .status-dot.red { background: #ff3b30; }
        .status-dot.blue { background: #0a84ff; }
        .status-dot.yellow { background: #ffd60a; }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .divider {
            height: 1px;
            background: linear-gradient(90deg, transparent, #333, transparent);
            margin: 12px 0;
        }

        .main-value {
            text-align: center;
            font-size: 56px;
            font-weight: 700;
            line-height: 1;
            margin: 20px 0;
            letter-spacing: -2px;
            text-shadow: 0 0 20px currentColor;
        }

        .main-value.large {
            font-size: 64px;
        }

        .info-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0;
            font-size: 13px;
        }

        .info-label {
            color: #888;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .info-value {
            font-weight: 600;
            color: #ffffff;
        }

        .pb-badge {
            display: inline-block;
            background: linear-gradient(135deg, #ffd700, #ffed4e);
            color: #000;
            padding: 2px 8px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 700;
            margin-left: 6px;
        }

        .button {
            background: linear-gradient(135deg, #0a84ff, #0066cc);
            color: white;
            border: none;
            padding: 14px 20px;
            border-radius: 24px;
            font-size: 15px;
            font-weight: 600;
            text-align: center;
            margin-top: auto;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(10, 132, 255, 0.4);
        }

        .button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(10, 132, 255, 0.6);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 12px 0;
        }

        .stat-box {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 10px;
            text-align: center;
        }

        .stat-label {
            font-size: 10px;
            color: #888;
            margin-bottom: 4px;
        }

        .stat-value {
            font-size: 18px;
            font-weight: 700;
            color: #fff;
        }

        .alert-banner {
            background: rgba(255, 59, 48, 0.2);
            border: 2px solid #ff3b30;
            border-radius: 16px;
            padding: 12px;
            text-align: center;
            margin: 12px 0;
            animation: alertPulse 1s infinite;
        }

        @keyframes alertPulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .alert-title {
            font-size: 13px;
            font-weight: 700;
            color: #ff3b30;
            margin-bottom: 6px;
        }

        .warning-banner {
            background: rgba(255, 214, 10, 0.15);
            border: 2px solid #ffd60a;
            border-radius: 16px;
            padding: 10px;
            text-align: center;
            margin: 12px 0;
        }

        .warning-title {
            font-size: 12px;
            font-weight: 700;
            color: #ffd60a;
            margin-bottom: 4px;
        }

        .success-badge {
            background: rgba(0, 255, 136, 0.15);
            border: 2px solid #00ff88;
            border-radius: 16px;
            padding: 10px;
            text-align: center;
            margin: 12px 0;
        }

        .success-title {
            font-size: 13px;
            font-weight: 700;
            color: #00ff88;
        }

        .timer-display {
            text-align: center;
            margin: 16px 0;
        }

        .timer-label {
            font-size: 11px;
            color: #888;
            margin-bottom: 6px;
        }

        .timer-value {
            font-size: 48px;
            font-weight: 700;
            color: #0a84ff;
            line-height: 1;
        }

        .bg-alert {
            background: linear-gradient(135deg, #1a0000, #330000) !important;
        }

        .bg-success {
            background: linear-gradient(135deg, #001a0a, #003314) !important;
        }

        .bg-warning {
            background: linear-gradient(135deg, #1a1700, #332e00) !important;
        }

        .setting-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .setting-label {
            font-size: 13px;
            color: #fff;
        }

        .setting-value {
            font-size: 14px;
            font-weight: 600;
            color: #0a84ff;
        }

        .legend {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 16px;
            padding: 20px;
            margin-top: 30px;
            color: #fff;
        }

        .legend h3 {
            font-size: 18px;
            margin-bottom: 16px;
            color: #0a84ff;
        }

        .legend-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 16px;
        }

        .legend-item {
            display: flex;
            align-items: flex-start;
            gap: 12px;
        }

        .legend-icon {
            width: 24px;
            height: 24px;
            border-radius: 6px;
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
        }

        .legend-text {
            flex: 1;
        }

        .legend-title {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .legend-desc {
            font-size: 11px;
            color: #888;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>⌚ FreeDivingLog - Apple Watch Ultra 2 UI Mockup</h1>
        
        <div class="screens-grid">
            <!-- 1. Home Screen -->
            <div class="watch-frame">
                <div class="screen-label">🏠 Home Screen</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>READY</span>
                    </div>
                    
                    <div style="text-align: center; margin-bottom: 16px;">
                        <div style="font-size: 18px; font-weight: 600;">👤 John Freediver</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">📊 PERSONAL BEST</div>
                        <div class="info-row">
                            <span class="info-label">🏆 Max Depth</span>
                            <span class="info-value">42.3m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏱️ Max Time</span>
                            <span class="info-value">3:45</span>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">⚙️ Quick Settings</div>
                        <div class="info-row">
                            <span class="info-label">🎯 Target</span>
                            <span class="info-value">40m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏲️ Recovery</span>
                            <span class="info-value">2:00</span>
                        </div>
                    </div>
                    
                    <button class="button">🌊 START DIVE</button>
                </div>
            </div>

            <!-- 2. Pre-Dive Screen -->
            <div class="watch-frame">
                <div class="screen-label">🔵 Pre-Dive</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>PRE-DIVE</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">📍 Location</span>
                        <span class="info-value" style="color: #00ff88;">Ready</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">🌡️ Water Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">⚙️ Session Settings</div>
                        <div class="info-row">
                            <span class="info-label">🎯 Target</span>
                            <span class="info-value">40m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏲️ Recovery</span>
                            <span class="info-value">2:00</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">🔔 Alerts</span>
                            <span class="info-value" style="color: #00ff88;">ON</span>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; margin-top: auto; padding: 16px 0; color: #00ff88; font-size: 13px;">
                        ✅ Ready to Dive<br>
                        <span style="font-size: 11px; color: #666;">(1m depth auto-start)</span>
                    </div>
                </div>
            </div>

            <!-- 3. Active Dive Screen -->
            <div class="watch-frame">
                <div class="screen-label">🟢 Active Dive</div>
                <div class="watch-screen bg-success">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>DIVING</span>
                    </div>
                    
                    <div class="main-value large" style="color: #00ff88;">38.5m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">⏱️ Time</span>
                        <span class="info-value" style="font-size: 18px;">2:15</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">🎯 Target</span>
                        <span class="info-value">40m</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">↑ Ascent</span>
                        <span class="info-value" style="color: #00ff88;">0.8 m/s</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row" style="font-size: 12px;">
                        <span class="info-label">💓 Heart</span>
                        <span class="info-value">65 bpm</span>
                    </div>
                    <div class="info-row" style="font-size: 12px;">
                        <span class="info-label">🌡️ Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                </div>
            </div>

            <!-- 4. Alert Screen -->
            <div class="watch-frame">
                <div class="screen-label">🔴 Alert</div>
                <div class="watch-screen bg-alert">
                    <div class="screen-header">
                        <span class="status-dot red"></span>
                        <span>ALERT!</span>
                    </div>
                    
                    <div class="main-value large" style="color: #ffffff;">38.5m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="alert-banner">
                        <div class="alert-title">⚠️ ASCENT SPEED</div>
                        <div style="font-size: 36px; font-weight: 700; color: #ff3b30; margin: 8px 0;">1.5 m/s</div>
                        <div style="font-size: 14px; font-weight: 700; color: #ff3b30;">TOO FAST!</div>
                    </div>
                    
                    <div style="text-align: center; color: #ff6b6b; font-size: 12px; margin-top: 16px;">
                        📳 Strong Haptic x3<br>
                        Slow down your ascent
                    </div>
                </div>
            </div>

            <!-- 5. Target Reached -->
            <div class="watch-frame">
                <div class="screen-label">🎯 Target Reached</div>
                <div class="watch-screen bg-success">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>TARGET!</span>
                    </div>
                    
                    <div class="main-value large" style="color: #00ff88;">40.0m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="success-badge">
                        <div class="success-title">✅ Goal Achieved!</div>
                        <div style="font-size: 11px; color: #888; margin-top: 4px;">Target depth reached</div>
                    </div>
                    
                    <div class="info-row" style="margin-top: 16px;">
                        <span class="info-label">⏱️ Time</span>
                        <span class="info-value" style="font-size: 18px;">2:20</span>
                    </div>
                    
                    <div style="text-align: center; color: #00ff88; font-size: 12px; margin-top: 16px;">
                        📳 Haptic x2<br>
                        <span style="color: #666;">Returns to dive mode in 1s</span>
                    </div>
                </div>
            </div>

            <!-- 6. Surface Mode -->
            <div class="watch-frame">
                <div class="screen-label">🌊 Surface</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SURFACE</span>
                    </div>
                    
                    <div style="text-align: center; font-size: 13px; color: #888; margin-bottom: 8px;">
                        Dive #3 Complete
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-box">
                            <div class="stat-label">Max Depth</div>
                            <div class="stat-value">40.2m <span class="pb-badge">PB</span></div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-label">Time</div>
                            <div class="stat-value">2:45</div>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="timer-display">
                        <div class="timer-label">⏲️ RECOVERY TIMER</div>
                        <div class="timer-value">1:35</div>
                        <div style="font-size: 11px; color: #666; margin-top: 4px;">(2:00 recommended)</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="font-size: 11px; color: #888; margin-top: 8px;">
                        <div class="info-row" style="font-size: 11px;">
                            <span>Session Stats:</span>
                        </div>
                        <div class="info-row" style="font-size: 11px;">
                            <span class="info-label">Dives</span>
                            <span class="info-value">3</span>
                        </div>
                        <div class="info-row" style="font-size: 11px;">
                            <span class="info-label">Max</span>
                            <span class="info-value">40.2m</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 7. Recovery Warning -->
            <div class="watch-frame">
                <div class="screen-label">⚠️ Recovery Warning</div>
                <div class="watch-screen bg-warning">
                    <div class="screen-header">
                        <span class="status-dot yellow"></span>
                        <span>SURFACE</span>
                    </div>
                    
                    <div class="timer-display">
                        <div class="timer-label">⏲️ RECOVERY</div>
                        <div class="timer-value" style="color: #ffd60a;">0:45</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="warning-banner">
                        <div class="warning-title">⚠️ Short Recovery</div>
                        <div style="font-size: 11px; color: #fff; margin-top: 6px;">
                            Recommended: 2:00<br>
                            Current: 0:45
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; font-size: 12px; color: #ffd60a; margin-top: 12px;">
                        ⚠️ Take more time<br>
                        <span style="font-size: 11px; color: #888;">for safety</span>
                    </div>
                    
                    <div style="text-align: center; color: #666; font-size: 10px; margin-top: 12px;">
                        📳 Soft Haptic x1
                    </div>
                </div>
            </div>

            <!-- 8. Session Summary -->
            <div class="watch-frame">
                <div class="screen-label">📊 Session Summary</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SESSION END</span>
                    </div>
                    
                    <div style="text-align: center; font-size: 20px; font-weight: 700; margin: 12px 0;">
                        Total Dives: 5
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">🏆 Max Depth</span>
                        <span class="info-value">40.2m <span class="pb-badge">PB</span></span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">⏱️ Max Time</span>
                        <span class="info-value">2:45</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">📊 Avg Depth</span>
                        <span class="info-value">35.8m</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">⏲️ Total Time</span>
                        <span class="info-value">12:30</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">🌡️ Water Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; color: #00ff88; font-size: 12px; margin: 12px 0;">
                        ✅ Synced to iPhone
                    </div>
                    
                    <button class="button" style="margin-top: 8px;">🏠 Back to Home</button>
                </div>
            </div>

            <!-- 9. Settings -->
            <div class="watch-frame">
                <div class="screen-label">⚙️ Settings</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SETTINGS</span>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🎯 Target Depth</div>
                        <div class="setting-value">→ 40m</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">⏲️ Recovery Time</div>
                        <div class="setting-value">→ 2:00</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🚀 Ascent Alert</div>
                        <div class="setting-value">→ 1.2 m/s</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🔔 Haptics</div>
                        <div class="setting-value" style="color: #00ff88;">ON</div>
                    </div>
                    
                    <div class="setting-row" style="border-bottom: none;">
                        <div class="setting-label">📏 Units</div>
                        <div class="setting-value">Meters</div>
                    </div>
                    
                    <div style="text-align: center; color: #666; font-size: 10px; margin-top: 16px;">
                        Use Digital Crown to adjust<br>
                        Tap to toggle ON/OFF
                    </div>
                </div>
            </div>
        </div>

        <!-- Legend -->
        <div class="legend">
            <h3>🎨 UI 디자인 가이드라인</h3>
            <div class="legend-grid">
                <div class="legend-item">
                    <div class="legend-icon" style="background: #00ff88;">🟢</div>
                    <div class="legend-text">
                        <div class="legend-title">정상 상태 (Green)</div>
                        <div class="legend-desc">안전한 다이빙 진행 중, 목표 달성</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ff3b30;">🔴</div>
                    <div class="legend-text">
                        <div class="legend-title">위험 경고 (Red)</div>
                        <div class="legend-desc">상승속도 초과, 즉시 조치 필요</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ffd60a;">🟡</div>
                    <div class="legend-text">
                        <div class="legend-title">주의 필요 (Yellow)</div>
                        <div class="legend-desc">회복시간 부족, 주의 권고</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #0a84ff;">🔵</div>
                    <div class="legend-text">
                        <div class="legend-title">정보/대기 (Blue)</div>
                        <div class="legend-desc">수면 상태, 준비 모드</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ffd700;">🏆</div>
                    <div class="legend-text">
                        <div class="legend-title">PB 달성 (Gold)</div>
                        <div class="legend-desc">개인 최고 기록 갱신</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #666;">📳</div>
                    <div class="legend-text">
                        <div class="legend-title">햅틱 피드백</div>
                        <div class="legend-desc">진동 강도: 강함(x3), 중간(x2), 약함(x1)

## DB 설
    class W_HOME,W_DIVE,W_SURF,W_SESSION,W_MONITOR,W_ALERT,W_RECOVERY,W_STORE,W_SYNC,W_DEPTH,W_HR,W_TEMP watchStyle
    class P_LOG,P_DETAIL,P_STATS,P_COMM,P_SET,P_SYNC,P_ANALYTICS,P_VIS,P_COMMUNITY,P_EXPORT,P_STORE,P_CLOUD,P_CACHE phoneStyle
    class B_GATE,B_USER,B_DIVE,B_SOCIAL,B_CHALLENGE,B_PUSH,B_MAP backendStyle
    class B_DB,B_REDIS,B_S3 dataStyle
    class B_RECOMMEND,B_INSIGHT aiStyle
