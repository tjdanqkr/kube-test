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

CREATE TABLE mydb1.Board (
id BINARY(16) NOT NULL,
title VARCHAR(255) NOT NULL,
content TEXT NOT NULL,
PRIMARY KEY (id)
);

CREATE TABLE mydb2.Comment ( id BINARY(16) NOT NULL, content TEXT NOT NULL, board_id BINARY(16) NOT NULL, PRIMARY KEY (id));
