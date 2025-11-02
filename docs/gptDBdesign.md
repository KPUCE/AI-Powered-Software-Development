```mermaid

erDiagram
    USER ||--o{ DIVE_SESSION : "has"
    USER ||--o{ DEVICE : "owns"
    DIVE_SESSION ||--|{ DIVE_SAMPLE : "contains"
    USER ||--o{ FRIEND : "connects"
    DIVE_SESSION ||--o{ ANALYSIS_RESULT : "generates"

    USER {
        uuid user_id PK
        string email
        string name
        string locale
        date created_at
        date last_login
    }

    DEVICE {
        uuid device_id PK
        uuid user_id FK
        string device_type
        string os_version
        date registered_at
    }

    DIVE_SESSION {
        uuid session_id PK
        uuid user_id FK
        timestamp start_time
        timestamp end_time
        float max_depth
        float avg_depth
        float total_time
        float recovery_time
        boolean synced
        string location_name
        geography gps_point
    }

    DIVE_SAMPLE {
        bigint sample_id PK
        uuid session_id FK
        timestamp ts
        float depth_m
        float temperature_c
        float ascent_speed
        boolean alert_flag
    }

    ANALYSIS_RESULT {
        uuid analysis_id PK
        uuid session_id FK
        string type  // ex: “recovery_efficiency”
        jsonb metrics
        timestamp created_at
    }

    FRIEND {
        uuid user_id FK
        uuid friend_id FK
        date created_at
        boolean accepted
    }
