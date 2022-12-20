```
rabbitmq_version=3.11.2-debian-11-r0
rabbitmq_user=demo
rabbitmq_password=demo
rabbitmq_url=rabbitmq.domain.com
rabbitmq_persistence_enabled=true
rabbitmq_persistence_size=2Gi
rabbitmq_replica=3
namespace=services
helm repo add bitnami https://charts.bitnami.com/bitnami
helm upgrade --install rabbitmq -f ./values.yaml \
--set image.tag=$(rabbitmq_version) \
--set auth.username=$(rabbitmq_user) \
--set auth.password=$(rabbitmq_password) \
--set auth.erlangCookie=Bl3lzVgcUI78HAazkebTng== \
--set ingress.enabled=true,ingress.hostname=$(rabbitmq_url) \
--set persistence.enabled=$(rabbitmq_persistence_enabled) \
--set persistence.size=$(rabbitmq_persistence_size) \
--set replicaCount=$(rabbitmq_replica) \
bitnami/rabbitmq --namespace $(namespace) --create-namespace 
```