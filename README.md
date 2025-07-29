```sequenceDiagram
    participant 사용자
    participant UploadManager
    participant EventQueue
    participant EventLooper
    participant ConvertModule
    participant LicenseModule
    participant Dashboard

    사용자->>UploadManager: 업로드 요청 (1:2)
    UploadManager->>EventQueue: UPLOAD_REQUEST 이벤트 등록
    EventLooper->>EventQueue: 이벤트 감시
    EventQueue-->>EventLooper: UPLOAD_REQUEST 이벤트 반환
    EventLooper->>Dashboard: 영상 대기중 상태 추가
    EventLooper->>EventQueue: CONVERT_START 이벤트 등록
    EventLooper->>ConvertModule: 변환 시작
    ConvertModule-->>EventQueue: CONVERT_END 이벤트 등록
    EventLooper->>EventQueue: LICENSE_START 이벤트 등록
    EventLooper->>LicenseModule: 검증 시작
    LicenseModule-->>EventQueue: LICENSE_END 이벤트 등록
    EventLooper->>Dashboard: STATUS_UPDATE 이벤트 전달
    Dashboard-->>사용자: 처리 현황 출력
```
