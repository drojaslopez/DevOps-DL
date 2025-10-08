# Módulo 4 - Observabilidad avanzada
## Equipo Vortex

### 1. ¿Cuál es la diferencia entre monitoreo y observabilidad?

    Monitoreo
        - Es ver el estado actual de un sistema a través de métricas predefinidas (CPU, memoria, latencia, errores, etc.).
        - Usa herramientas como Prometheus y Grafana para recolectar y visualizar datos.
        - Responde preguntas como: “¿Está funcionando bien ahora?”

    Observabilidad
        - Es un concepto más amplio: permite entender por qué ocurre algo en el sistema.
        - No solo revisa métricas, también incluye logs y trazas distribuidas (ej. con OpenTelemetry, Jaeger, Tempo).
        - Responde preguntas más profundas como: “¿Por qué este servicio está lento?” o “Dónde está el cuello de botella en los microservicios?”.

    En Resumen:
        - Monitoreo = mirar síntomas (qué pasa).
        - Observabilidad = investigar causas (por qué pasa).

### 2. ¿Qué rol cumple Prometheus en un sistema observable?

    Prometheus cumple un rol clave dentro de la observabilidad, porque es la herramienta que se encarga de recolectar, almacenar y consultar métricas en series temporales.

    - Prometheus se conecta a los servicios mediante endpoints y guarda métricas como consumo de CPU, memoria, latencia o número de peticiones.
    - Permite definir alertas personalizadas para detectar problemas automáticamente.
    - Es ampliamente usado en Kubernetes, servicios web y sistemas distribuidos.

    En Resumen:
        - Prometheus es como el sensor del sistema:
        - Recolecta datos de rendimiento.
        - Almacena las métricas históricas.
        - Activa alertas cuando algo anda mal.
        - Se integra con herramientas como Grafana, que lo complementa mostrando dashboards visuales.

👉      En un sistema observable, Prometheus es el motor de monitoreo de métricas, que junto con logs y trazas completa la triada de la observabilidad.

### 3. ¿Para qué se utiliza Grafana y cómo se relaciona con Prometheus?

        ¿Para qué se utiliza Grafana?
            - Grafana es una herramienta de visualización de datos.
            - Permite crear dashboards interactivos donde se muestran gráficas, alertas y paneles en tiempo real.
            - Hace que los datos técnicos (métricas, logs, trazas) sean fáciles de interpretar y analizar.

        ¿Cómo se relaciona con Prometheus?
            - Prometheus recolecta y guarda las métricas (base de datos de series temporales).
            - Grafana se conecta a Prometheus y muestra esas métricas en gráficos y paneles personalizables.
            - Juntos forman un ecosistema:
                - Prometheus = Recolecta datos.
                - Grafana = Los muestra de forma visual.
        
        En Resumen:
        Grafana es la pantalla y Prometheus es el sensor. Uno mide, el otro lo hace entendible.

### 4. ¿Qué es OpenTelemetry y por qué es relevante en entornos distribuidos?

    ¿Qué es OpenTelemetry?
        - Es un estándar abierto para recolectar datos de observabilidad: métricas, logs y trazas.
        - Proporciona librerías e integraciones para muchos lenguajes (Java, Python, Node.js, Go).
        - Permite enviar esos datos a herramientas como Jaeger, Grafana Tempo, Prometheus, etc.

    ¿Por qué es relevante en entornos distribuidos?
        - En sistemas modernos con microservicios, una petición pasa por muchos servicios distintos (frontend → API → base de datos → otro servicio).
        - Sin un estándar, cada servicio usaría una forma distinta de recolectar información → difícil de entender.
        - OpenTelemetry unifica la instrumentación: todos los servicios recolectan datos de la misma forma, lo que facilita:
        - Tener una visión completa del rendimiento del sistema.
        - Detectar cuellos de botella y errores entre servicios.
        - Simplificar la integración con distintas herramientas de monitoreo y trazabilidad.

    En Resumen:
        OpenTelemetry es como un idioma común que hablan todos los microservicios para reportar qué hacen, cuánto tardan y si fallan. Eso lo hace fundamental para entender el “todo” en un entorno distribuido.

### 5. ¿Cuál es la utilidad de una traza distribuida en el diagnóstico de errores?

    ¿Qué es una traza distribuida?
        - Es el camino completo que sigue una petición (request) al pasar por distintos servicios de un sistema distribuido (ej. frontend → API → base de datos → microservicio X).
        - Se representa como un “mapa” con los tiempos y estados de cada paso

    ¿Cuál es su utilidad en el diagnóstico de errores?
        - Detectar cuellos de botella → si un servicio tarda mucho, la traza lo muestra.
        - Identificar el punto exacto del fallo → no solo sabes que “algo falló”, sino dónde falló.
        - Analizar dependencias entre servicios → útil en microservicios, donde un error puede estar escondido en la interacción.
        - Reducir el tiempo de resolución de incidentes → los equipos encuentran más rápido la causa raíz.

    En Resumen:
        Una traza distribuida es como el GPS de una petición: te muestra por dónde pasó, cuánto demoró en cada lugar y dónde se rompió.

### 6. ¿En qué casos usarías Jaeger o Tempo y cuál es su diferencia principal?

    ¿Cuándo usar Jaeger o Tempo?
        - Los usarías cuando necesitas trazabilidad distribuida para:
        - Seguir el recorrido de una petición en arquitecturas de microservicios.
        - Diagnosticar latencias y errores que no aparecen en simples métricas.
        - Entender cómo interactúan tus servicios en producción.

    Jaeger
        - Proyecto original de tracing distribuido creado por Uber.
        - Muy usado en la comunidad y se integra con OpenTelemetry.
        - Ideal si necesitas debugging detallado de cada request, con buena interfaz web.

    Tempo (Grafana Tempo)
        - Proyecto de Grafana Labs.
        - Está diseñado para escalar a gran volumen de trazas sin necesidad de guardar todos los datos en una base de datos pesada.
        - Se integra nativamente con el ecosistema Grafana (dashboards, métricas de Prometheus, logs de Loki).

    Diferencia principal
        - Jaeger: pensado más para análisis profundo de trazas individuales.
        - Tempo: pensado para escenarios de alto volumen, integrándose de forma liviana con métricas y logs en Grafana.

    En Resumen:
        - Usa Jaeger si quieres detalles finos de cada request.
        - Usa Tempo si necesitas manejar millones de trazas y verlas junto a métricas/logs en Grafana.

### 7. ¿Qué ventajas ofrece el uso conjunto de Prometheus, Grafana y OpenTelemetry en una arquitectura moderna?

    Ventajas de usar Prometheus + Grafana + OpenTelemetry en conjunto

    a. Visión integral del sistema
        - Prometheus recolecta métricas (CPU, memoria, peticiones).
        - OpenTelemetry recolecta logs y trazas.
        - Grafana integra todo en dashboards unificados, mostrando métricas, logs y trazas en un mismo lugar.

    b. Detección y diagnóstico más rápido
        - Prometheus te alerta: “hay alta latencia”.
        - Grafana te muestra gráficamente cuándo empezó.
        - OpenTelemetry + Jaeger/Tempo te dicen dónde está el cuello de botella exacto.

    c. Estándar abierto y flexible
        - OpenTelemetry permite que distintos servicios (Java, Python, Node.js, Go, etc.) reporten datos de forma consistente.
        - Esto evita depender de una sola herramienta propietaria.

    d. Escalabilidad en arquitecturas modernas
        - En Kubernetes y microservicios, donde hay cientos de pods y servicios, esta combinación facilita tener observabilidad real y en tiempo real.

    e. Mejor capacidad de respuesta ante incidentes
        - Equipos de DevOps y SRE pueden pasar de “el sistema está lento” a “la latencia viene del servicio de pagos, en la consulta SQL” en minutos, no horas.

    En Resumen:
        - Prometheus = mide.
        - Grafana = muestra.
        - OpenTelemetry = explica el porqué.
        
        Juntos forman una plataforma completa de observabilidad, que permite detectar, entender y resolver problemas rápidamente en sistemas distribuidos modernos.
        