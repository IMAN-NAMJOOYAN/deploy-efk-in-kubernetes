# deploy-efk-in-kubernetes
**Deploy EFK (Elasticsearch Fluentbit Kibana) in Kubernetes**

**LOM:**
App|Version
---|---
kubenetes|1.26.5
elasticsearch|7.17.13
kibana|7.17.13
fluentbit|2.1.10



1- Create kube-logging namespace
```
kubectl apply -f 01-create-ns.yaml
```
2- Create secret for username and password.

*Note: username and pasword must be base64 format.*
```
kubectl apply -f elastics-secret.yaml
```
3- Create elasticsearch service.
```
kubectl apply -f 02-elastic-service.yaml
```
4- Create elasticsearch statefulset.
```
kubectl apply -f 03-elastic-statefulset.yaml
```
5- Create kibana service.
```
kubectl apply -f 04-kibana-service.yaml
```
6- Create kibana Deployment.
```
kubectl apply -f 05-kibana-deployment.yaml
```
7- Create fluentbit service.
```
kubectl apply -f 06-fluent-bit-service.yaml
```
8- Create fluentbit configmap.
```
kubectl apply -f 07-fluent-bit-configmap.yaml
```
9- Create fluentbit daemonset.
```
kubectl apply -f 08-fluent-bit-daemonset.yaml
```

**Create Kibana nginx Ingress with basic authentication (Optional)**

1- Creating auth file with username and password:
```
USER=<USERNAME_HERE>; PASSWORD=<PASSWORD_HERE>; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth

Example:
  USER=elastic; PASSWORD=Admin1234 echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth
```
2- Creating a secret based on file auth.
```
kubectl -n kube-logging create secret generic kibana-basic-auth --from-file=auth
```
3- Deploy nginx ingress for kibana:
```
kubectl apply -f ingress-kibana.yaml
```

**Login to Kibana**

![image](https://github.com/IMAN-NAMJOOYAN/deploy-efk-in-kubernetes/assets/16554389/ee9abd2b-ffbd-47c9-8399-0296a9851677)


![image](https://github.com/IMAN-NAMJOOYAN/deploy-efk-in-kubernetes/assets/16554389/dc349148-b05e-4c37-8b58-a1b88bbad1b4)


