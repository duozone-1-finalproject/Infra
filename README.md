# Infra
infra-repo/
├── base/                      # 공통 기본 리소스 (네임스페이스, 스토리지 등)
│   ├── namespace.yaml
│   ├── storage-class.yaml
│   └── common-configmap.yaml  # 필요 시
│
├── overlays/                  # 환경별 설정 (dev, staging, prod)
│   ├── dev/
│   │   └── kustomization.yaml
│   ├── staging/
│   │   └── kustomization.yaml
│   └── prod/
│       └── kustomization.yaml
│
└── services/                  # 각 서비스별 쿠버네티스 리소스 모음
    ├── kafka/
    │   ├── kafka-deployment.yaml
    │   ├── kafka-service.yaml
    │   └── zookeeper-deployment.yaml
    │
    ├── redis/
    │   ├── redis-deployment.yaml
    │   └── redis-service.yaml
    │
    ├── nginx/
    │   ├── nginx-deployment.yaml
    │   └── nginx-ingress.yaml
    │
    ├── backend/
    │   ├── deployment.yaml
    │   └── service.yaml
    │
    └── ai/
        ├── deployment.yaml
        └── service.yaml



1. redis/ 폴더
Redis 서버 관련 쿠버네티스 리소스(YAML) 파일 모음

Redis는 보통 캐시나 세션 저장소로 쓰이는 인프라 서비스야

예: redis-deployment.yaml, redis-service.yaml 같은 파일들이 여기 들어감

2. base/ 폴더
쿠버네티스 리소스의 공통 기본 설정 모음

네임스페이스, 스토리지 클래스, 공통 ConfigMap, RBAC 등

여러 서비스가 공유하는 기본 리소스를 따로 분리해 관리하는 곳

예:

namespace.yaml (모든 서비스가 배포될 네임스페이스 정의)

storage-class.yaml (스토리지 정책)

3. overlays/ 폴더
kustomize 환경별(Dev, Staging, Prod 등) 오버레이 설정

기본 base/ 설정을 가져와서 환경별로 다르게 설정(리플리카 수, 이미지 태그 등) 적용

예:

overlays/dev/kustomization.yaml → 개발환경에 맞춘 설정

overlays/prod/kustomization.yaml → 운영환경에 맞춘 설정

# Helm 저장소 추가 (없으면)
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

# ingress-nginx 설치 (myapp 네임스페이스에 설치 예시)
kubectl create namespace ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx


kustomize를 사용하면 YAML 파일을 중복 없이 효율적으로 관리할 수 있음

