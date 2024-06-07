# calico

https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart

# loadbalancer MetalLB
https://cla9.tistory.com/94

# ingress-controller-nginx
https://kubernetes.github.io/ingress-nginx/deploy/


helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update

helm install nginx-ingress ingress-nginx/ingress-nginx

확인

kubectl get pods -n default -l app.kubernetes.io/name=ingress-nginx

minikube tunnel 미니 쿠버일때

kubectl get pods -n default -l app.kubernetes.io/name=ingress-nginx

kubectl get svc -n default nginx-ingress-ingress-nginx-controller
```
...
spec:
clusterIP: 10.107.23.205
clusterIPs:

- 10.107.23.205
  externalIPs:
- 내부
  ...
```
kubectl get ing -A

kubectl describe ing my-ingress -n ingress-nginx

kubectl describe ingress my-ingress -n my-namespace

kubectl logs -l app.kubernetes.io/name=ingress-nginx -n default

mysql1
CREATE TABLE mydb1.Board (
id BINARY(16) NOT NULL,
title VARCHAR(255) NOT NULL,
content TEXT NOT NULL,
PRIMARY KEY (id)
);

mysql2

CREATE TABLE mydb2.Comment ( id BINARY(16) NOT NULL, content TEXT NOT NULL, board_id BINARY(16) NOT NULL, PRIMARY KEY (id));

https://kubernetes.github.io/ingress-nginx/user-guide/ingress-path-matching/

pathValue 사용

---

# kube-metric

https://github.com/kubernetes-sigs/metrics-server
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
I0717 12:19:32.132722 1 server.go:187] "Failed probe" probe="metric-storage-ready" err="no metrics to serve"
E0717 12:19:39.159422 1 scraper.go:140] "Failed to scrape node" err="Get \"https://192.168.49.2:10250/metrics/resource\": x509: cannot validate certificate for 192.168.49.2 because it doesn't contain any IP SANs" node="minikube"
```
kubectl patch deployment metrics-server -n kube-system --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'
```
---

# helm
https://helm.sh/docs/intro/install/

helm create back1

cd back1

rm templates

템플릿을 사용안하고 안에 여러가지 디펜던시 만들어 사용할 거라 삭제

change Chart.yaml

디펜던시 설정 해줘야함

cd charts

helm create back1

helm create db-1

안에 만들고

Values.yaml 설정


helm install back1 back1 -n back

helm install back2 back2 -n back

뭔가 바뀔 때 

helm upgrade back2 back2 -n back

여러가지 설정은 안에 있음

---

# argocd
https://argo-cd.readthedocs.io/en/stable/getting_started/

intstall

kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl edit svc argocd-server -n argocd
```
ports:
- name: http
  nodePort: 30001
  port: 80
  protocol: TCP
  targetPort: 8080
- name: https
  nodePort: 31397
  port: 443
  protocol: TCP
  targetPort: 8080
  selector:
  app.kubernetes.io/name: argocd-server
  sessionAffinity: None
  type: NodePort
```
https://localhost:30001/login?return_url=https%3A%2F%2Flocalhost%3A30001%2Fapplications

kubectl exec -it argocd-server-697df9f478-v4chh /bin/bash -n argocd

argocd admin initial-password -n argocd

password 출력

id admin
password password


