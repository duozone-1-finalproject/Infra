# Helm 설치
helm install elasticsearch elastic/elasticsearch --infra elasticsearch --create-infra --set replicas=1

# 설치 확인 명령어
kubectl get all -n elasticsearch
