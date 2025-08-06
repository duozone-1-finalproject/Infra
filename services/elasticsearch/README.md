# Helm 설치
helm install elasticsearch elastic/elasticsearch --namespace elasticsearch --create-namespace --set replicas=1

# 설치 확인 명령어
kubectl get all -n elasticsearch
