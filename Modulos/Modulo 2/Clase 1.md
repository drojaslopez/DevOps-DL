curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/

https://github.com/argoproj/argocd-example-apps

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

minikube start --driver=docker

kubectl port-forward svc/argocd-server -n argocd 8080:443


echo $POD_NAME
>> $POD_NAME = (kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o jsonpath='{.items[0].metadata.name}')
kubectl -n argocd get secret argocd-initial-admin-secret `
>>   -o jsonpath="{.data.password}" |
>>   % { [Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($_)) }