# Módulo 5 - Kubernetes avanzado
## Equipo Vortex

### 1. ¿Qué ventajas ofrece Helm frente al uso directo de manifiestos YAML?

        Helm ofrece varias ventajas importantes sobre el uso manual de manifiestos YAML en Kubernetes:
        
        a. Simplifica la instalación y actualización de aplicaciones
            En lugar de aplicar muchos archivos YAML uno por uno, Helm permite instalar una aplicación completa con un solo comando (helm install), incluyendo todos sus recursos (pods, services, deployments, etc.).

        b. Uso de “charts” reutilizables y versionados
            Los charts de Helm funcionan como plantillas empaquetadas que puedes reutilizar en diferentes entornos (desarrollo, pruebas, producción) sin tener que reescribir los YAML.

        c. Gestión de versiones y rollback fácil
            Helm guarda el historial de despliegues. Si una actualización falla, puedes volver a una versión anterior con un solo comando (helm rollback).

        d. Parámetros dinámicos y configuraciones centralizadas
            Permite cambiar valores específicos (como variables de entorno, puertos o réplicas) sin modificar los YAML originales, usando archivos values.yaml.

        e. Automatización y consistencia
            Asegura que las aplicaciones se desplieguen siempre de la misma forma en diferentes entornos, reduciendo errores humanos.

        En resumen:
            Helm convierte el proceso manual y repetitivo de aplicar múltiples manifiestos YAML en un flujo más ordenado, automatizado y controlado, ideal para equipos DevOps que buscan consistencia, trazabilidad y rapidez en sus despliegues.

### 2. ¿Qué es un Kubernetes Operator y en qué se diferencia de un controlador estándar?

        Un Kubernetes Operator es una extensión avanzada de Kubernetes que automatiza la gestión de aplicaciones complejas dentro del clúster.
        Podemos pensar en un Operator como un “administrador automático” que entiende cómo instalar, configurar, actualizar y mantener una aplicación específica.

        Cómo funciona

        El Operator combina dos cosas:

        a. Controlador personalizado (Custom Controller): vigila el estado del sistema (por ejemplo, una base de datos) y actúa para mantenerlo como se desea.
        b. Custom Resource Definition (CRD): define nuevos tipos de objetos de Kubernetes, por ejemplo PostgresCluster o RedisInstance, que representan esa aplicación.

        De esta forma, el Operator observa los recursos personalizados y ejecuta acciones automáticas (como hacer backups, restauraciones o actualizaciones) cuando es necesario.

        Diferencias con un controlador estándar

        - Función principal:
            Controlador Estandar: Mantener el estado deseado de recursos nativos de Kubernetes (como Pods, Deployments, Services).
            Operator: Gestionar aplicaciones complejas o con estado propio (como bases de datos o sistemas distribuidos).

        - Alcance:
            Controlador: Recursos básicos del clúster.
            Operator: Aplicaciones específicas, con lógica de negocio incorporada.

        - Automatización avanzada:
            Controlador: Limitada al ciclo de vida básico (crear, actualizar, borrar).
            Operator: Incluye operaciones inteligentes como backups, recuperación, escalado o configuración dinámica.

        - Personalización:
            Controlador: No tiene conocimiento de aplicaciones concretas.
            Operator: Contiene conocimiento experto sobre cómo operar una aplicación específica.

        En resumen:
            Un Operator amplía las capacidades de Kubernetes, permitiendo que el propio clúster “sepa” cómo administrar aplicaciones complejas de manera automática y confiable, reduciendo la necesidad de intervención manual.

### 3. ¿Qué prácticas de seguridad básicas se deben aplicar a pods en Kubernetes?

        La seguridad en Kubernetes debe aplicarse desde el nivel más básico, y los pods son uno de los puntos más importantes.
        Estas son las prácticas esenciales que se deben seguir:
        
        a. Controlar el acceso con RBAC (Role-Based Access Control)
            - Usa roles y bindings para limitar quién puede crear, modificar o eliminar pods.
            - Evita usar cuentas con permisos de administrador salvo que sea estrictamente necesario.
            - Objetivo: aplicar el principio de “mínimos privilegios”.

        b. Restringir permisos dentro de los contenedores
            - Evita ejecutar contenedores como root.
            - Usa el campo securityContext en los manifiestos YAML para establecer usuarios no privilegiados.
            - Desactiva capacidades innecesarias del sistema (capabilities).
            - Objetivo: reducir el riesgo de escalamiento de privilegios.

        c. Aplicar Network Policies
            - Define Network Policies para controlar qué pods pueden comunicarse entre sí o con el exterior.
            - Esto evita que un pod comprometido acceda libremente a toda la red del clúster.
            - Objetivo: segmentar la red y limitar el movimiento lateral.

        d. Validar configuraciones y políticas
            - Usa herramientas como OPA (Open Policy Agent) o Kyverno para validar que los pods cumplan reglas de seguridad (por ejemplo, que no se ejecuten como root o que usen imágenes verificadas).
            - Objetivo: garantizar que solo se desplieguen configuraciones seguras.

        e. Escanear imágenes y controlar secretos
            - Escanea regularmente las imágenes de contenedores en busca de vulnerabilidades.
            - No guardes contraseñas o llaves directamente en variables de entorno: usa Secrets de Kubernetes y habilita TLS entre servicios.
            - Objetivo: proteger datos sensibles y evitar fugas de información.

        En resumen:
            Para mantener seguros los pods en Kubernetes, hay que limitar permisos, aislar redes, validar configuraciones y proteger credenciales.
            Estas prácticas reducen los riesgos de ataques y garantizan una operación más confiable del clúster.

### 4. ¿Cómo se gestiona el control de acceso en Kubernetes?

        El control de acceso en Kubernetes se gestiona principalmente mediante el sistema RBAC (Role-Based Access Control), que permite definir quién puede hacer qué dentro del clúster.

        a. RBAC: Roles y permisos
            - Roles: definen qué acciones se pueden realizar (por ejemplo, crear pods, ver logs o eliminar servicios).
            - RoleBindings: asignan esos roles a usuarios, grupos o cuentas de servicio.
            - Ejemplo: Un rol puede permitir ver pods (get, list) pero no eliminarlos (delete).

        b. Alcance de los roles
            - Role: se aplica dentro de un namespace específico.
            - ClusterRole: se aplica a todo el clúster.
            
            Esto permite diferenciar entre permisos locales (por ejemplo, solo en el namespace dev) y globales (para administradores o herramientas de despliegue).

        e. Cuentas de servicio (Service Accounts)
            - Los pods pueden usar Service Accounts para autenticarse frente a la API de Kubernetes.
            - Se recomienda asignar a cada aplicación su propia cuenta con permisos mínimos necesarios.

        f. Autenticación y autorización
            - Autenticación: verifica quién eres (usuario, grupo o servicio).
            - Autorización: verifica qué puedes hacer (por medio de roles y reglas).
            - También se puede usar Admission Controllers para revisar o rechazar peticiones antes de que se apliquen.

        En resumen:
            Kubernetes usa RBAC para otorgar permisos específicos a usuarios o aplicaciones, asegurando que cada uno tenga solo los privilegios necesarios.
            Este sistema ayuda a mantener un entorno seguro, ordenado y con control total de accesos dentro del clúster.

### 5. ¿Qué mecanismos existen para aislar redes entre pods o namespaces?

        Kubernetes utiliza un modelo de red plano por defecto, lo que significa que todos los pods pueden comunicarse entre sí sin restricciones.
        Sin embargo, cuando se busca mayor seguridad y control, existen varios mecanismos que permiten aislar el tráfico entre pods o namespaces.

        a. Network Policies (políticas de red)
            - Son el mecanismo principal para controlar el tráfico entre pods y namespaces.
            - Permiten definir quién puede comunicarse con quién (entradas y salidas).
            - Por ejemplo, se puede indicar que solo los pods del namespace frontend puedan hablar con los del namespace backend.
            - Objetivo: aislar y proteger servicios sensibles.

        b. CNI Plugins (Container Network Interface)
            - Kubernetes usa plugins de red (CNI) para gestionar la conectividad.
            - Algunos CNI avanzados, como Calico, Cilium o Weave Net, ofrecen funciones extra de seguridad y segmentación de tráfico.
            - Ejemplo: Calico permite definir políticas de red a nivel de capa 3/4 (IP y puertos) y capa 7 (aplicación).

        c. Namespaces como separación lógica
            - Los namespaces permiten dividir los recursos del clúster por equipos, entornos o aplicaciones.
            - Aunque por defecto no aíslan la red, pueden combinarse con Network Policies para lograr un aislamiento real entre ellos.
            - Ejemplo: el namespace dev no podrá comunicarse con prod si se aplican políticas restrictivas.

        d. Ingress y Egress controlados
            - Los Ingress Controllers gestionan el tráfico externo que entra al clúster.
            - También se puede controlar el Egress (salida de pods hacia internet) usando reglas específicas o firewalls del CNI.
            - Objetivo: filtrar conexiones y evitar fugas de datos.

        En resumen:
            - El aislamiento de redes en Kubernetes se logra combinando:
            - Network Policies (para definir reglas de comunicación),
            - CNI plugins (como Calico o Cilium),
            - y namespaces (para separar entornos lógicamente).
            
            Estos mecanismos aseguran que cada servicio o aplicación se comunique solo con quien debe hacerlo, fortaleciendo la seguridad y la estabilidad del clúster

### 6. ¿Qué ventajas ofrece el uso de un Service Mesh como complemento a la gestión de red en Kubernetes?

        Un Service Mesh es una capa adicional que se instala dentro del clúster de Kubernetes para gestionar y controlar el tráfico entre servicios de manera más inteligente y segura.
        En lugar de que cada aplicación maneje su propia lógica de comunicación, el Service Mesh lo hace por ella, de forma transparente.

        a. Observabilidad avanzada
            - Permite monitorear todas las llamadas entre servicios (service-to-service).
            - Muestra métricas como latencia, errores y tráfico, lo que ayuda a detectar problemas de red o rendimiento rápidamente.
            - Ejemplo: con herramientas como Istio o Linkerd, puedes ver qué microservicios están fallando o generando cuellos de botella.

        b. Seguridad mejorada
            - Implementa autenticación mutua (mTLS) entre servicios para cifrar todo el tráfico interno.
            - Aplica políticas de acceso centralizadas, evitando que un servicio no autorizado se comunique con otro.
            - Objetivo: proteger las comunicaciones internas sin modificar el código de las aplicaciones.

        c. Control del tráfico
            - Permite redirigir, balancear o limitar el tráfico entre servicios sin tocar el código.
            - Se pueden aplicar estrategias de despliegue seguras como canary releases, A/B testing o blue-green deployments.
            - Ejemplo: enviar solo un 10% del tráfico a una nueva versión para probarla antes del lanzamiento completo.

        d. Simplificación de la lógica en las aplicaciones
            - Las aplicaciones ya no necesitan manejar aspectos como reintentos, timeouts o circuit breakers — el Service Mesh lo hace automáticamente.
            - Beneficio: menos código complejo y más enfoque en la lógica de negocio.

        En resumen:
            - Un Service Mesh complementa la gestión de red de Kubernetes al ofrecer:
            - Mayor observabilidad
            - Seguridad de extremo a extremo
            - Control inteligente del tráfico y simplificación operativa

            Es una herramienta clave para entornos de microservicios avanzados, donde la comunicación entre componentes debe ser confiable, segura y fácil de monitorear.

### 7. ¿Cómo manejaría una actualización de versión en un chart Helm sin afectar el entorno productivo?

    Aquí hay una propuesta de un plan claro y seguro para actualizar un chart Helm sin afectar producción:

    a. Prepara la versión
        - Sube version y (si aplica) appVersion en Chart.yaml.
        - Define un values-staging.yaml con la nueva imagen/tag y parámetros para pruebas.
        
        Helm permite versionar y actualizar aplicaciones empaquetadas como charts, manteniendo configuraciones por entorno

    b. Valida antes de tocar clústeres
        - helm lint (valida el chart)
        - helm template (renderiza YAML localmente para revisar)
        - (Opcional) helm diff upgrade ... (previsualiza cambios respecto a lo desplegado)

    c. Despliega primero en un entorno “seguro”
        - Usa otro namespace o otro release (p. ej. miapp-staging):
            helm upgrade --install miapp-staging ./chart \
            -n staging -f values-staging.yaml --wait --atomic

            [*] --wait espera a que todo quede listo.
            [*] --atomic revierte automáticamente si algo falla.
        - Buenas prácticas del módulo: mantener consistencia entre entornos y automatizar despliegues/rollbacks.

    d. Prueba y observa
        - Smoke tests, métricas y logs.
        - Si usas Service Mesh/Ingress, haz canary (enviar un % pequeño de tráfico a la nueva versión) o blue-green (dos versiones en paralelo y conmutación del tráfico).

    e. Promoción controlada a producción
        - Aplica el mismo chart con values-prod.yaml:
            helm upgrade --install miapp ./chart \
            -n prod -f values-prod.yaml --wait --atomic
        - Mantén los mismos manifests entre ambientes y solo cambia valores (evita “drift”).

    f. Plan de reversa (rollback)
        - Si algo sale mal en prod:
            helm rollback miapp <revision>
        (Helm guarda el historial de releases, lo que facilita volver atrás).

    g. (Opcional) GitOps
        - Gestiona el chart y values en Git y usa Argo CD para promover de staging a prod con pull requests y aprobaciones (consistencia y trazabilidad entre entornos).

    En Resumen:
        Resumen: empaqueta cambios como nueva versión de chart, valida localmente, despliega primero en staging con --wait --atomic, verifica observabilidad, realiza canary/blue-green si puedes, y promueve a prod con rollback listo. Esto aprovecha la gestión de versiones, entornos y actualizaciones que Helm ofrece para minimizar el riesgo en producción.

    