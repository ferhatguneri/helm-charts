```
redis_version=7.0.5-debian-11-r7
redis_password=demo
redis_replica_replicaCount=3
namespace=services
helm repo add bitnami https://charts.bitnami.com/bitnami
helm upgrade --install redis -f ./values.yaml \
--set image.tag=$(redis_version) \
--set auth.password=$(redis_password) \
--set replica.replicaCount=$(redis_replica_replicaCount) \
bitnami/redis -n $(namespace) --create-namespace
```