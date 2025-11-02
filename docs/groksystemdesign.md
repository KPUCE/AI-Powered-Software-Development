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
        BM3계
