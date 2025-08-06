# Infra Repository

이 리포지토리는 쿠버네티스 기반 인프라 리소스들을 관리하기 위한 구성으로, `kustomize`를 활용해 환경별로 효율적인 배포 및 유지보수가 가능하도록 설계되었습니다.

## 📁 디렉토리 구조

Infra/
├── base/ # 공통 리소스
├── overlays/ # 환경별 설정 (dev, staging, prod)
├── services/ # 서비스별 리소스 정의 (Kafka, Redis, Nginx 등)


---

### 1. `base/`

- **공통 리소스** (모든 환경에서 공유)
  - `namespace.yaml`: 네임스페이스 정의
  - `storage-class.yaml`: 스토리지 클래스 정책
  - `common-configmap.yaml`: 공통 환경 설정 (필요 시)

---

### 2. `services/`

- **각 서비스별 쿠버네티스 리소스 정의**
  - `kafka/`: Kafka & Zookeeper 배포 리소스
  - `redis/`: Redis 캐시 서버 배포 리소스
  - `nginx/`: Nginx Ingress Controller 관련 설정
  - `backend/`: 백엔드 서비스 배포 리소스
  - `ai/`: AI 서비스 배포 리소스

---

### 3. `overlays/`

- **환경별 오버레이 설정 (`kustomize`)**
  - `dev/`, `staging/`, `prod/`
  - 각 환경에 맞는 설정 (예: replica 수, 이미지 태그 등) 적용 가능
  - 공통 리소스는 `base/`에서 불러와 사용

---

## ✅ Kustomize 사용법

예시) 개발 환경(`dev`) 배포

```bash
kubectl apply -k overlays/dev



