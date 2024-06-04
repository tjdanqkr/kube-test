ingress-controller-nginx
https://kubernetes.github.io/ingress-nginx/deploy/

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update

helm install nginx-ingress ingress-nginx/ingress-nginx

확인

kubectl get pods -n default -l app.kubernetes.io/name=ingress-nginx

minikube tunnel 미니 쿠버일때

kubectl get pods -n default -l app.kubernetes.io/name=ingress-nginx

kubectl get svc -n default nginx-ingress-ingress-nginx-controller

kubectl port-forward svc/nginx-ingress-ingress-nginx-controller 8080:80 -n default

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

https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart

kube-metric

https://github.com/kubernetes-sigs/metrics-server

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

I0717 12:19:32.132722 1 server.go:187] "Failed probe" probe="metric-storage-ready" err="no metrics to serve"
E0717 12:19:39.159422 1 scraper.go:140] "Failed to scrape node" err="Get \"https://192.168.49.2:10250/metrics/resource\": x509: cannot validate certificate for 192.168.49.2 because it doesn't contain any IP SANs" node="minikube"

kubectl patch deployment metrics-server -n kube-system --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'
