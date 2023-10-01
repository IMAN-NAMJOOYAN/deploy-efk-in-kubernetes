# deploy-efk-in-kubernetes
**Deploy EFK (Elasticsearch Fluentbit Kibana) in Kubernetes**
1- Create kube-logging namespace.
```
kubectl apply -f 01-create-ns.yaml
```
2- Create elasticsearch service.
```
kubectl apply -f 02-elastic-service.yaml
```
3- Create elasticsearch statefulset.
```
kubectl apply -f 03-elastic-statefulset.yaml
```
4- Create kibana service.
```
kubectl apply -f 04-kibana-service.yaml
```
5- Create kibana Deployment.
```
kubectl apply -f 05-kibana-deployment.yaml
```
6- Create fluentbit service.
```
kubectl apply -f 06-fluent-bit-service.yaml
```
7- Create fluentbit configmap.
```
kubectl apply -f 07-fluent-bit-configmap.yaml
```
8- Create fluentbit daemonset.
```
kubectl apply -f 08-fluent-bit-daemonset.yaml
```

