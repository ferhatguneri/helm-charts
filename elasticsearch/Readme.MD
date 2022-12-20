```
kibana_url=kibana.domain.com
namespace=services
elastic_version=8.4.1
elastic_persistence_size=8Gi
elastic_password=demo
sed -i "s|{{kibana_url}}|$(kibana_url)|" elasticsearch/elk.yaml
sed -i "s|{{namespace}}|$(namespace)|" elasticsearch/elk.yaml
sed -i "s|{{elastic_version}}|$(elastic_version)|" elasticsearch/elk.yaml
sed -i "s|{{elastic_persistence_size}}|$(elastic_persistence_size)|" elasticsearch/elk.yaml
kubectl create -f https://download.elastic.co/downloads/eck/2.1.0/crds.yaml
kubectl apply -f https://download.elastic.co/downloads/eck/2.1.0/operator.yaml
kubectl create ns $(namespace)
kubectl create secret generic elasticsearch-es-elastic-user --from-literal=elastic=$(elastic_password) -n $(namespace)
kubectl apply -f ./elasticsearch.yaml
kubectl apply -f ./kibana.yaml
```
