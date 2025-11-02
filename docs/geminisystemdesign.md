## 시스템 설계도

graph TD
    subgraph Apple Watch Ultra 2 (DIVE CLIENT & SENSOR HUB)
        A[F2. Dive Session Auto Detect] --> B(F3/F4. Real-time Monitoring & Safety Alert Engine);
        D[Watch Sensors: Depth, Time, CoreMotion, GPS] --> A;
        D --> B;
        B --> C{F7. Local Session Storage (CoreData/SQLite)};
        C --> E[Watch Connectivity (WC Session)];
    end

    subgraph iPhone (MAIN CLIENT & ANALYTICS HUB)
        E --> F[WC Receiver & Data Sync Service];
        F --> G{F8. Central Log Database (CoreData)};
        G --> H[F10. Analytics & AI Coaching Module];
        G --> I[F11. Community/Map Module];
        G --> J[F12. Settings & iCloud Management];
    end

    subgraph Cloud Services (BACKEND & EXTERNAL SERVICE)
        J --> K[F12. iCloud/Cloud Storage];
        I --> L[External Map/POI DB];
        H --> M[AI/ML Model for Training Recommendation];
    end

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
