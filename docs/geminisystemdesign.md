## 시스템 설계도

```mermaid

graph TD

    %% Apple Watch
    subgraph AWU2["Apple Watch Ultra 2 (DIVE CLIENT & SENSOR HUB)"]
        A["F2. Dive Session Auto Detect"] --> B["F3/F4. Real-time Monitoring & Safety Alert Engine"]
        D["Watch Sensors: Depth, Time, CoreMotion, GPS"] --> A
        D --> B
        B --> C["F7. Local Session Storage (CoreData/SQLite)"]
        C --> E["Watch Connectivity (WC Session)"]
    end

    %% iPhone
    subgraph iPhoneHub["iPhone (MAIN CLIENT & ANALYTICS HUB)"]
        E --> F["WC Receiver & Data Sync Service"]
        F --> G["F8. Central Log Database (CoreData)"]
        G --> H["F10. Analytics & AI Coaching Module"]
        G --> I["F11. Community/Map Module"]
        G --> J["F12. Settings & iCloud Management"]
    end

    %% Cloud
    subgraph Cloud["Cloud Services (BACKEND & EXTERNAL SERVICE)"]
        J --> K["iCloud / Cloud Storage"]
        I --> L["External Map / POI DB"]
        H --> M["AI/ML Model for Training Recommendation"]
    end

    %% Styles
    style A fill:#f9f,stroke:#333
    style B fill:#fcc,stroke:#f66,stroke-width:2px
    style C fill:#ccf,stroke:#333
    style E fill:#aaf,stroke:#333
    style F fill:#9f9,stroke:#333
    style G fill:#9cf,stroke:#333
    style H fill:#ff9,stroke:#333
    style I fill:#f9c,stroke:#333
    style J fill:#ccc,stroke:#333
    style K fill:#ddd,stroke:#333
    style L fill:#eee,stroke:#333
    style M fill:#fee,stroke:#333

```

## DB 설계

```mermaid
erDiagram
    USERS ||--o{ SESSIONS : "owns"
    USERS ||--o{ SETTINGS : "has"
    USERS ||--o{ BUDDIES : "initiates"
    USERS }|--|| BUDDIES : "as buddy"
    SESSIONS ||--o{ DIVES : "contains"
    BUDDIES }o--o{ SESSIONS : "shares (via JSONB)"

    USERS {
        UUID id PK
        VARCHAR email
        VARCHAR name
        TIMESTAMP created_at
    }
    SESSIONS {
        UUID id PK
        UUID user_id FK
        DATE date
        JSONB location
        INTERVAL total_time
    }
    DIVES {
        UUID id PK
        UUID session_id FK
        DECIMAL depth
        INTEGER duration
        DECIMAL ascent_speed
    }
    SETTINGS {
        UUID id PK
        UUID user_id FK
        DECIMAL alert_depth
        INTEGER recovery_time
    }
    BUDDIES {
        UUID id PK
        UUID user_id FK
        UUID buddy_user_id FK
        JSONB shared_sessions
    }
```


---

## UI 설계

## ⌚️ Apple Watch Ultra 2 UI 시안

요청하신 **FreeDivingLog** 앱의 Apple Watch Ultra 2용 핵심 화면 UI 목업입니다.

---

### 1. 홈/준비 화면 (Home/Pre-Dive Screen)

프리다이버의 PB와 현재 세션 통계를 보여주는 시작 화면입니다.



---

### 2. 다이빙 실시간 모니터링 화면 (Real-time Dive Monitor)

다이빙 중 실시간 수심, 시간, 안전 경고를 표시하는 화면입니다.



---

### 3. 표면 회복 타이머 화면 (Surface Interval Timer)

수면 복귀 후 회복 시간 관리 및 직전 다이브 기록을 보여주는 화면입니다.


