```
longhorn_url=longhorn.domain.com
longhorn_reclaimPolicy=Retain
longhorn_password=demo
longhorn_user=demo
helm repo add longhorn https://charts.longhorn.io
helm install longhorn --wait --timeout 15m \
--set ingress.host=$(longhorn_url) \
--set ingress.enabled=true \
--set persistence.reclaimPolicy=$(longhorn_reclaimPolicy) \
longhorn/longhorn --namespace longhorn-system --create-namespace
echo "$(longhorn_user):$(openssl passwd -stdin -apr1 <<< $(longhorn_password))" >> auth
kubectl -n longhorn-system create secret generic basic-auth --from-file=auth
sed -i "s|{{longhorn_url}}|$(longhorn_url)|" ./ingress.yaml
kubectl apply -f ./ingress.yaml
```