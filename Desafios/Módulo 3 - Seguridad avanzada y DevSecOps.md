# Módulo 3 - Seguridad avanzada y DevSecOps
## Equipo Vortex

### 1 ¿Qué es DevSecOps y cómo se diferencia de DevOps tradicional?

    DevOps tradicional busca integrar a los equipos de desarrollo (Dev) y operaciones (Ops) para entregar software de forma más rápida, automatizada y continua. El foco principal está en la velocidad de despliegue, la colaboración entre equipos y la automatización del ciclo de vida del software.

    DevSecOps es la evolución de DevOps que agrega la seguridad (Sec) desde el inicio del ciclo de vida del software. En lugar de revisar vulnerabilidades al final (cuando el software ya está en producción), se integran controles de seguridad en cada fase:

        - Planificación: definición de políticas de seguridad.
        - Codificación: escaneo de dependencias y librerías inseguras (ej: Snyk).
        - Construcción y pruebas: análisis de imágenes de contenedor y archivos de configuración (ej: Trivy, Checkov).
        - Despliegue y operación: gestión segura de secretos (ej: Vault), políticas de red, RBAC y monitoreo continuo.

    De esta forma, DevSecOps reduce la superficie de ataque, detecta vulnerabilidades tempranas y promueve una cultura de seguridad compartida entre desarrollo, QA y operaciones
    En Resumen:
        - DevOps = rapidez + colaboración + automatización.
        - DevSecOps = lo mismo, pero añadiendo seguridad desde el principio, sin esperar al final.

### 2 ¿Qué tipo de análisis realiza Trivy y en qué etapas puede integrarse?

    Trivy es una herramienta de escaneo de seguridad que detecta vulnerabilidades y configuraciones inseguras en diferentes componentes del ecosistema DevOps:
        1. Imágenes de contenedores → analiza las capas de las imágenes Docker en busca de vulnerabilidades conocidas en paquetes y dependencias.
        2. Repositorios de código → detecta dependencias inseguras en proyectos (Node.js, Python, Java, etc.).
        3. Archivos de configuración → revisa Dockerfiles, manifiestos de Kubernetes (YAML/Helm) para encontrar malas prácticas de seguridad.
        4. Infraestructura como Código (IaC) → identifica configuraciones inseguras en Terraform, CloudFormation, Kubernetes, etc.

        Etapas donde puede integrarse Trivy en un flujo DevOps/DevSecOps
        
        Trivy es muy flexible y puede usarse en varias fases del ciclo de vida:
            1. Fase de codificación / construcción
                - Escaneo de dependencias del proyecto.
                - Validación de Dockerfiles y configuración antes de compilar la imagen.
            2. Fase de integración continua (CI)
                - Integrado en pipelines (GitHub Actions, GitLab CI, Jenkins, etc.) para analizar imágenes recién construidas.
                - Evita que una build con vulnerabilidades críticas llegue a producción.
            3. Fase de despliegue (CD)
                - Escaneo de manifiestos de Kubernetes o Helm antes de aplicar cambios al clúster.
            4. Fase de operación / producción
                - Monitoreo periódico de imágenes ya desplegadas en clústeres, ya que las vulnerabilidades se descubren con el tiempo.

### 3 ¿Cómo ayuda Checkov a mejorar la seguridad de la infraestructura como código?

    Es una herramienta de análisis estático para IaC (Infrastructure as Code) que revisa plantillas y configuraciones en Terraform, CloudFormation, Kubernetes YAML, ARM Templates, Pulumi, entre otros.

    ¿Cómo ayuda a mejorar la seguridad?

        1. Detecta malas prácticas antes del despliegue
            - Ejemplo: detectar buckets S3 públicos, grupos de seguridad con puertos abiertos, claves sin cifrar, roles con permisos excesivos.
        2. Aplica políticas de seguridad como código
            - Permite definir reglas (con políticas propias o librerías ya incluidas) para que todo despliegue cumpla estándares de seguridad de la organización.
        3. Automatiza auditorías de IaC
            - Se integra en pipelines de CI/CD para evitar que configuraciones inseguras lleguen a producción.
        4. Cumplimiento normativo
            - Ayuda a cumplir estándares como CIS, GDPR, HIPAA, PCI-DSS, al verificar que la infraestructura se ajuste a esas guías.

    Etapas de integración en el ciclo DevSecOps

        1. Codificación → el desarrollador ejecuta Checkov localmente para validar su Terraform/Kubernetes antes de hacer commit.
        2. Integración continua (CI) → se ejecuta en pipelines (GitHub Actions, GitLab CI, Jenkins) para bloquear configuraciones inseguras.
        3. Revisión de cambios → Checkov genera reportes claros que facilitan auditorías de seguridad.
    
    En Resumen:
        Checkov mejora la seguridad de la IaC al analizar y detectar configuraciones inseguras en Terraform, Kubernetes y otras plantillas antes del despliegue. Automatiza auditorías, aplica políticas de seguridad como código y evita que vulnerabilidades lleguen a producción.

### 4 ¿Qué ventajas ofrece Vault frente a otras formas de gestionar secretos?

    Vault (de HashiCorp) es una herramienta diseñada para almacenar, gestionar y controlar el acceso a secretos (contraseñas, tokens, certificados, claves API, etc.) de forma segura.

    Ventajas frente a otras formas de gestionar secretos (archivos .env, variables de entorno, repositorios privados, etc.):

        1. Cifrado centralizado y seguro
            - Todos los secretos se almacenan cifrados.
            - Evita exponer contraseñas en texto plano en archivos o repositorios.

        2. Control de acceso granular (RBAC y políticas)
            - Permite definir quién puede acceder a qué secreto.
            - Se integra con sistemas de identidad (LDAP, Kubernetes, AWS IAM, etc.).

        3. Rotación automática de secretos
            - Vault puede generar contraseñas y tokens dinámicos, que expiran después de cierto tiempo.
            - Ejemplo: un usuario obtiene una credencial de base de datos válida solo por 1 hora.

        4. Auditoría y trazabilidad
            - Registra quién accedió a cada secreto y cuándo, lo que facilita auditorías de seguridad.

        5. Compatibilidad con múltiples entornos
            - Funciona en pipelines CI/CD, contenedores, microservicios, Kubernetes y entornos cloud.
    
    Ejemplo práctico:
        - En lugar de guardar claves API en un archivo .env o en variables de entorno, Vault entrega la clave al servicio solo cuando la necesita y con un tiempo de vida limitado.
        - Si un atacante roba la clave, esta ya puede estar expirada → reduce el impacto de filtraciones.

    En Resumen:
        Vault ofrece ventajas como almacenamiento cifrado, control de acceso granular, rotación automática de secretos, auditoría y compatibilidad multiplataforma, superando métodos tradicionales como .env o repositorios privados, que son menos seguros y más difíciles de gestionar.

### 5 . ¿Qué riesgos se mitigan al evitar que los secretos estén en manifiestos YAML o variables de entorno?

    Riesgos mitigados al NO guardar secretos en YAML o variables de entorno:
        1. Exposición accidental en repositorios
            - Si los secretos están en archivos YAML o .env, pueden ser subidos a GitHub/GitLab por error.
            - Esto los deja expuestos públicamente o a cualquier miembro del equipo con acceso al repo.

        2. Fugas en logs o monitoreo
            - Variables de entorno y manifiestos pueden ser registrados en logs de CI/CD, crash reports o sistemas de monitoreo → filtración involuntaria de credenciales.

        3. Acceso no controlado
            - Cualquiera con acceso al archivo YAML o a las variables de entorno puede ver los secretos en texto plano.
            - No hay control de quién accede, cuándo y para qué.

        4. Dificultad en la rotación de credenciales
            - Si los secretos están "hardcodeados" en manifiestos o variables, hay que hacer commits y redeploy cada vez que cambian.
            - Esto aumenta la probabilidad de errores y filtraciones.

        5. Persistencia innecesaria en memoria
            - Variables de entorno pueden ser accedidas por procesos comprometidos en el mismo host o contenedor, aumentando el riesgo si un atacante gana acceso parcial.

    En Resumen:
        Al evitar guardar secretos en manifiestos YAML o variables de entorno se mitigan riesgos como:
            - Filtraciones accidentales en repositorios o logs,
            - Exposición en texto plano sin control de accesos,
            - Rotación difícil y poco segura,
            - Mayor superficie de ataque en caso de compromisos de contenedores o procesos.

### 6. ¿Cómo se puede asegurar un clúster Kubernetes frente a configuraciones por defecto?

    Las configuraciones por defecto de Kubernetes suelen ser demasiado permisivas, lo que abre puertas a ataques. Para endurecer la seguridad se recomienda:

        1. Control de acceso (RBAC)
            - Configurar Role-Based Access Control para dar el mínimo permiso necesario (principio de least privilege).
            - Evitar usar la cuenta cluster-admin salvo casos críticos.

        2. Namespaces y aislamiento
        - Separar workloads por namespaces.
        - Aplicar resource quotas y limit ranges para evitar abuso de recursos.

        3. Políticas de red
            - Aplicar NetworkPolicies para restringir el tráfico entre pods, evitando que todos puedan comunicarse libremente.
        
        4. Seguridad en pods y contenedores
            - Usar PodSecurity Standards o herramientas como OPA Gatekeeper o Kyverno para validar manifiestos.
            - Evitar ejecutar contenedores como root.
            - Usar readOnlyRootFilesystem y limitar capacidades de Linux.
        
        5. Escaneo de imágenes
            - Integrar herramientas como Trivy o Snyk para detectar vulnerabilidades en las imágenes antes de desplegar.

        6. Gestión de secretos
            - No guardar secretos en YAML ni en variables de entorno.
            - Usar Vault u otros Secret Managers integrados con Kubernetes.

        7. Certificados y autenticación
            - Rotar certificados y claves regularmente.
            - Integrar Kubernetes con un proveedor de identidad (ej: LDAP, OIDC).

        8. Monitoreo y auditoría
            - Activar Audit Logs de Kubernetes.
            - Usar herramientas de observabilidad (Prometheus, Falco, etc.) para detectar actividades sospechosas.

    En Resumen:
        Un clúster Kubernetes se asegura frente a configuraciones por defecto aplicando RBAC mínimo necesario, namespaces aislados, políticas de red, validación de manifiestos (OPA/Kyverno), ejecución sin root, escaneo de imágenes, gestión segura de secretos, rotación de certificados y monitoreo/auditoría continua.

### 7. ¿Cómo integrarías Snyk en el ciclo de desarrollo para proyectos Node.js o Python?

    Snyk analiza dependencias de proyectos (Node.js, Python, Java, etc.) para detectar vulnerabilidades conocidas, y sugiere versiones seguras o parches.

    Etapas de integración en el ciclo DevSecOps

        1. Fase de desarrollo local
            - Instalar el CLI de Snyk (npm install -g snyk o pip install snyk).
            - Los desarrolladores pueden ejecutar snyk test para analizar dependencias en package.json (Node.js) o requirements.txt (Python).
            - Esto detecta librerías vulnerables antes de hacer commit.

        2. Fase de control de versiones (repositorio Git)
            - Configurar Snyk para monitorear el repo (GitHub, GitLab, Bitbucket).
            - Snyk analiza automáticamente cada pull request y genera comentarios con vulnerabilidades detectadas y posibles fixes.

        3. Fase de integración continua (CI/CD)
            - Añadir un paso en el pipeline (Jenkins, GitHub Actions, GitLab CI, etc.):
                - name: Run Snyk Security Scan
                  run: snyk test
            - Se puede usar snyk monitor para enviar los resultados al panel de Snyk y hacer seguimiento en el tiempo.
            - Si encuentra vulnerabilidades críticas, puede bloquear el despliegue.

        4. Fase de despliegue y operación
            - Snyk puede integrarse con contenedores (Docker/Kubernetes) para escanear imágenes antes de publicarlas.
            - Así no solo se analizan dependencias del código, sino también vulnerabilidades en el sistema base.

    Em Resumen:
        Para proyectos Node.js o Python, Snyk se integra en el ciclo de desarrollo:
            - En desarrollo local: snyk test sobre dependencias (package.json o requirements.txt).
            - En repositorios: monitoreo automático en pull requests.
            - En CI/CD: escaneo en pipelines con snyk test y snyk monitor.
            - En despliegue: análisis de imágenes de contenedores para asegurar que nada vulnerable llegue a producción.

