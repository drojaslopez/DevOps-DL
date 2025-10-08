Invoke-WebRequest -Uri "https://github.com/istio/istio/releases/download/1.23.0/istio-1.23.0-win.zip" -OutFile "istio.zip"
Expand-Archive -Path "istio.zip" -DestinationPath "." -Force
$env:Path = "$($pwd.Path)\bin;$($env:Path)"
istioctl install --set profile=demo -y
kubectl label namespace default istio-injection=enabled

Jesus Mitchell Quintero 22:25
se está quejando de propiedades que no son compatibles con la versión del manifiesto (Gateway, por ejemplo)

Guido Perez 22:25
deberíamos lograr esto ?

Carlos Tapia - Docente 22:35
kubectl port-forward svc/istio-ingressgateway -n istio-system 8080:80

Guido Perez 22:41
Istio es super completo, trae addons de Kiali, Grafana, Jaeger y Prometheus 👌