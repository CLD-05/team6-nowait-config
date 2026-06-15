# team6-nowait-config

> **Team 6 `nowait` 서비스의 인프라 및 애플리케이션 배포 설정을 관리하는 GitOps 저장소입니다.** > Helm Chart를 통해 애플리케이션을 패키징하고, ArgoCD를 이용해 개발(dev) 및 운영(prod) 환경에 선언형으로 배포를 동기화합니다.

<br>

## 📂 디렉토리 구조 (Directory Structure)

```text
team6-nowait-config/
├── charts/                           # 서비스별 안정화된 Helm 패키지 템플릿
│   ├── nowait-api/                   # API 애플리케이션 Helm Chart
│   │   ├── Chart.yaml
│   │   ├── values.yaml               # 기본 설정 파일
│   │   └── templates/                # K8s 리소스 매니페스트 템플릿
│   │       ├── deployment.yaml
│   │       ├── service.yaml
│   │       ├── ingress.yaml
│   │       ├── hpa.yaml
│   │       ├── external-secret.yaml  # AWS Secrets Manager 연동용 자격 증명
│   │       └── pdb.yaml              # Pod Disruption Budget (가용성 보장)
│   └── nowait-worker/                # Worker 애플리케이션 Helm Chart
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│           ├── deployment.yaml
│           ├── hpa.yaml
│           └── external-secret.yaml
├── envs/                             # 환경별 대상 오버라이드 값 (Values)
│   ├── dev/                          # Development 환경 설정
│   │   ├── api-values.yaml
│   │   └── worker-values.yaml
│   └── prod/                         # Production 환경 설정
│       ├── api-values.yaml
│       └── worker-values.yaml
└── argocd/                           # ArgoCD Application 매니페스트
    ├── dev-api-application.yaml
    ├── dev-worker-application.yaml
    ├── prod-api-application.yaml
    └── prod-worker-application.yaml
