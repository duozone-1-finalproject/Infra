# 1. Helm 저장소 등록 및 최신화

   helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
   helm repo update

# 2. NGINX Ingress Controller 설치

   kubectl create namespace ingress-nginx


helm install ingress-nginx ingress-nginx/ingress-nginx -n infra
기본값으로 설치되며, 필요한 설정은 Helm 값 파일(values.yaml)로 커스터마이징 가능

# 3. 설치 확인

   kubectl get pods -n ingress-nginx
   kubectl get svc -n ingress-nginx
   ingress-nginx-controller Pod와 LoadBalancer/NodePort 타입 Service가 생성됨

# 4. 서비스에 대한 Ingress 리소스 작성 (예: backend, ai)
   infra/services/nginx/ingress.yaml 같은 파일로 관리


# 5. Ingress 리소스 배포
   kubectl apply -f infra-repo/services/nginx/ingress.yaml
