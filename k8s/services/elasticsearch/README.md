# 사전 helm 체크
helm repo add elastic https://helm.elastic.co
helm repo update

# Helm 설치
helm install elasticsearch elastic/elasticsearch -n infra --set replicas=1

