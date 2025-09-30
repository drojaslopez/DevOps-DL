nosotros usabamos .env y variables de entornos en aws , pero existe alguna otra forma de manejarlas ?

Jorge Cárcamo 21:54
A veces los dev las imprimen con console.log para debuguear ☠️

Jesus Mitchell Quintero 21:58
duplicidad de código también revisa
ayer tuve que lidiar con un node v 12 🙁 
pero hay una opción si es con Docker, servirla sobre una imagen distroless

Pablo Ubeda 22:03
"Quien lo hizo ya esta en Fundación Las Rosas" - Anónimo

Jorge Cárcamo 22:03
Docker Scout sirve también como herramienta de análisis de seguridad y vulnerabilidade d imágenes

Oscar Angulo 22:03
Son súper caros los de aws

Carlos Tapia - Docente 22:11
https://github.com/snyk-labs/nodejs-goof

Carlos Tapia - Docente 22:13
npm install -g snyl
snyk auth
snyk test

Oscar Angulo 22:15
Hay que hacer fork del repo?
Aa ok

Ivo Landa 22:15
😵

Y esto se puede automatizar con gihub actions por ejemplo?
Claro pero después genera un reporte algo? que accion tomo sobre las vulnerabilidades que encuentra?
Aaaa ok
Pero podriamos frenar la generación de la imagen por ejemplo o un rollback si encuentra algo
Ta weno
Si pero ya poder detener la generación o enviar una alerta esta bueno

Dixon Aróstica 22:18
soporta varios lenguajes esta buena

Jesus Mitchell Quintero 22:18
para eso ya hay que conectar con un agente y un LLM por debajo, para que corrija


soporta varios lenguajes esta buena

Jesus Mitchell Quintero 22:18
para eso ya hay que conectar con un agente y un LLM por debajo, para que corrija

Oscar Angulo 22:20
Pero esas correcciones complicado automátizarlas igual porque derepente en un cambio de version de un codigo se deprecan funciones o desaparecen y ahi se rompe la compilacion

Jesus Mitchell Quintero 22:20
el mes pasado Sonarqube introdujo PR's generados por IA en base a los análisis (hay que conectar con openAI propio)

Oscar Angulo 22:23
Que comando ejecuto profe?

Sebastián 22:23
npm install -g snyl

snyk auth

snyk test

docker build -t node-good . 

trivy image node-goof

Carlos Tapia - Docente 22:23
trivy image node-goof

Oscar Angulo 22:23
vale


pip install checkov
checkov -d .