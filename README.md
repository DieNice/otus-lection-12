# otus-lection-12


```sh
helm install nginx ingress-nginx/ingress-nginx \
  --namespace lection-12 \
  --create-namespace \
  --set controller.service.type=NodePort \
  --set controller.service.nodePorts.http=30080
```


```sh
kubectl create namespace lection-12 && helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/ && helm repo update && helm install nginx ingress-nginx/ingress-nginx --namespace lection-12 -f .helm/nginx-ingress.yaml 

kubectl delete validatingwebhookconfiguration ingress-nginx-admission

kubectl patch svc -n lection-12 nginx-ingress-nginx-controller -p '{"spec":{"type":"LoadBalancer"}}'

kubectl apply -f .helm/tempalates/ 

minikube tunnel предназначен для сервисов типа LoadBalancer. Когда сервис имеет тип NodePort, tunnel игнорирует его, потому что:
NodePort уже открывает порт на виртуальной машине minikube (30080)

Tunnel нужен только чтобы дать IP адрес (обычно 127.0.0.1) для LoadBalancer

minikube tunnel
```

```sh
kubectl get svc -n lection-12

echo "127.0.0.1 arch.homework" >> /etc/hosts

curl -L http://arch.homework/api/v1/health/
curl -L http://arch.homework/otusapp/dienice/health 

```