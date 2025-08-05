# 1. Helm 저장소 등록 및 최신화

   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   helm repo update

# 2. NGINX Ingress Controller 설치

   kubectl create namespace ingress-nginx

helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
기본값으로 설치되며, 필요한 설정은 Helm 값 파일(values.yaml)로 커스터마이징 가능

# 3. 설치 확인

   kubectl get pods -n ingress-nginx
   kubectl get svc -n ingress-nginx
   ingress-nginx-controller Pod와 LoadBalancer/NodePort 타입 Service가 생성됨

# 4. 서비스에 대한 Ingress 리소스 작성 (예: backend, ai)
   infra-repo/services/nginx/ingress.yaml 같은 파일로 관리

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: myapp-ingress
namespace: myapp
annotations:
nginx.ingress.kubernetes.io/rewrite-target: /
spec:
rules:
- host: backend.example.com
  http:
  paths:
    - path: /
      pathType: Prefix
      backend:
      service:
      name: backend-service
      port:
      number: 80
- host: ai.example.com
  http:
  paths:
    - path: /
      pathType: Prefix
      backend:
      service:
      name: ai-service
      port:
      number: 81
5. Ingress 리소스 배포
   bash
   복사
   편집
   kubectl apply -f infra-repo/services/nginx/ingress.yaml
6. Helm 설치 시 값 커스터마이징 (선택)
   values.yaml 파일 만들어서 예를 들어 로깅, 리소스 제한, 서비스 타입 등을 조절 가능

yaml
복사
편집
controller:
replicaCount: 2
service:
type: LoadBalancer
resources:
limits:
cpu: 200m
memory: 256Mi
requests:
cpu: 100m
memory: 128Mi
설치 시:

bash
복사
편집
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx -f values.yaml
