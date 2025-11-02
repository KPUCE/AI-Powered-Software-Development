## 시스템 설계도

```mermaid
graph TD
    %% === Apple Watch Ultra 2 (실시간 + 오프라인 전용) ===
    subgraph "Apple Watch Ultra 2 (오프라인 우선, 실시간 모니터링)"
        direction TB
        WM1["Sensors Module\n(CoreMotion: Depth, Temp)"]
        WM2["Dive Engine\n(Auto Detect, Session Mgmt)"]
        WM3["Real-time Monitor\n(Depth, Time, Speed)"]
        WM4["Alert Engine\n(Haptic, Speed >1.2m/s)"]
        WM5["Recovery Timer\n(Surface Rest)"]
        WM6["Local Logger\n(CoreData Cache)"]
        WM7["Sync Agent\n(WatchConnectivity)"]
    end

    %% === iPhone (분석 + 동기화 + UX 허브) ===
    subgraph "iPhone (분석, 시각화, 설정 관리)"
        direction TB
        IM1["Sync Manager\n(WatchConnectivity)"]
        IM2["Data Processor\n(Validation, Merge)"]
        IM3["Analytics Engine\n(Stats, Trends, Graphs)"]
        IM4["AI Coach\n(CoreML: Recovery, Progress)"]
        IM5["Visualization\n(Swift Charts, Depth-Time)"]
        IM6["Settings Manager\n(UserDefaults + iCloud)"]
        IM7["Community Module\n(Buddy Share, Dive Spots)"]
        IM8["Cloud Sync\n(iCloudKit / Documents)"]
    end

    %% === Backend (서버리스 iCloud) ===
    subgraph "Backend (Serverless) (iCloud - Apple Managed)"
        direction TB
        BM1["iCloud Sync Engine\n(CKRecord, File Sync)"]
        BM2["iCloud Backup\n(Auto Backup/Restore)"]
        BM3["iCloud Sharing\n(Private Share Links)"]
    end

    %% === 데이터 흐름 ===
    WM1 --> WM2
    WM2 --> WM3
    WM3 --> WM4
    WM3 --> WM5
    WM3 --> WM6
    WM6 --> WM7
    WM7 <-->|"BLE / Background Sync\n(<10s on connect)"| IM1

    IM1 --> IM2
    IM2 --> IM3
    IM3 --> IM5
    IM3 --> IM4
    IM4 --> IM5
    IM6 <--> IM1
    IM7 --> IM8
    IM8 <--> BM1
    BM1 <--> BM2
    BM1 <--> BM3

    %% 양방향 설정 동기화
    IM6 <-->|"iCloud Key-Value"| BM1

    %% HealthKit 공유 (옵션)
    WM1 -.->|Heart Rate| HK[HealthKit]
    IM3 -.->|"Workout Sync"| HK

    %% 스타일
    classDef watch fill:#e3f2fd,stroke:#1976d2,stroke-width:2px,color:#000
    classDef phone fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#000
    classDef cloud fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#000
    classDef external fill:#f3e5f5,stroke:#7b1fa2,stroke-width:1px

    class WM1,WM2,WM3,WM4,WM5,WM6,WM7 watch
    class IM1,IM2,IM3,IM4,IM5,IM6,IM7,IM8 phone
    class BM1,BM2,BM3 cloud
    class HK external
```

---

