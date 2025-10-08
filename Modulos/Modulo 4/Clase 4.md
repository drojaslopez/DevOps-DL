https://github.com/cTapiaDev/mastering_devops_g2

docker build -t mi-app:v1
kind load docker-image mi-app:v1


kubectl apply -f app-deployment.yaml

kubectl create configmap prometheus-config -n monitoring --from-file=prometheus.yml=prometheus-config.yaml

kubectl apply -f prometheus-deployment.yaml

kubectl port-forward -n monitoring svc/prometheus-service 9091:9090