kubectl apply -f grafana-deployment.yaml

Javi 21:32
@Carlos Tapia - Docente , los comandos los dejas en el.repo en Git, si?

Carlos Tapia - Docente 21:32
kubectl port-forward -n monitoring svc/grafana 3000:3000

Carlos Tapia - Docente 21:36
http://prometheus-service.monitoring.svc.cluster.local:9090

Dixon Aróstica 21:48
super buena herramienta

Ivo Landa 21:54
Es vital el monitoreo de costos!

Erick Turpie 21:57
pfsense cuenta ? xD

Jorge Cárcamo 21:57
Network policies
Los rbac

Jesus Quintero Ruiz 21:58
cuando no están bien definidos los límites de recursos para los despliegues, y cuando escalan pueden causar lentitud en el cluster

Ivo Landa 22:02
Es un proceso progresivo! es importante considerarlo como en un roadmap similar de Producto

Jesus Quintero Ruiz 22:02
lo que hacemos nosotros es que puedes desplegar sin tests solo en ambiente de desarrollo, para poder llegar a QA son obligatorios y el pipeline te bloquea

Raul Farias S. 22:02
Pero para una POC no es necesario tener todo con test…

Ivo Landa 22:03
Equilibrio, siempre es necesario!

Raul Farias S. 22:04
Las POC son desechables… ni siquiera se sabe si esa POC será aprobada o no… perder tiempo en los test de una POC no lo veo viable

Usted 22:10
Si, fue en una empresa en la que trabaje

Jorge Cárcamo 22:13
Para grafana + Loki + prometheus ya existe un chart con el stack completo, llegar y completar el values.yaml

Jesus Quintero Ruiz 22:22
comienza con Docker

Jorge Cárcamo 22:22
Pequeñita dominio acotado —> serverless (lambda, functions, cloud run, etc)

Usted 22:23
existirá alguna métrica como guía?
si

Jesus Quintero Ruiz 22:23
Docker > Docker Compose >> Docker Swarm >> cluster

Usted 22:24
pero ahí mido por cantidad de contenedores
?

Carlos Tapia - Docente 22:26
kubectl create namespace mi-app-segura
helm repo add bitnami hhtps://charts.bitnami.com/bitnami

Carlos Tapia - Docente 22:31
helm install mi-redis bitnami/redis -n mi-app-segura -f redis-values.yaml

Jorge Cárcamo 22:32
helm repo update


kubectl apply -f cliente-y-red.yaml
docker pull busybox
kind load docker-image busybox