MÓDULO 7 
25. ¿Qué ventajas ofrece el uso de módulos en Terraform y cómo favorecen la escalabilidad en entornos multi-entorno (dev, prod, etc.)? 

 El uso de módulos en Terraform ofrece varias ventajas clave que se relacionan directamente con las buenas prácticas de Infraestructura como Código

Ventajas Principales:
    Reutilización de Código: Permiten empaquetar configuraciones de infraestructura en componentes reutilizables, evitando la duplicación de código entre entornos.
    Abstracción y Encapsulamiento: Ocultar la complejidad de la implementación, permitiendo a los equipos consumir infraestructura como "cajas negras" con interfaces bien definidas.
    Consistencia: Aseguran que todos los entornos sean idénticos en configuración, reduciendo los problemas de "funciona en mi máquina".
    Mantenibilidad: Los cambios se realizan en un solo lugar y se propagan a través de todos los entornos que usan el módulo.
    
Para Escalabilidad Multi-entorno:
    Parámetros por Entorno: Usando variables, un mismo módulo puede ser configurado de manera diferente para cada entorno (tamaño de instancias, capacidad, etc.).
    Estructura de Directorios Clara:
        environments/
        ├── dev/
        │   └── main.tf
        ├── staging/
        │   └── main.tf
        └── prod/
        └── main.tf
        modules/
        └── mi-recurso/
            └── main.tf

Registros de Módulos Remotos: Permiten versionar y compartir módulos entre equipos, facilitando la estandarización a gran escala.
Workspaces o Backends Diferentes: Permiten aislar el estado entre entornos mientras se mantiene la misma configuración base.
Variables de Entorno y Archivos .tfvars: Facilitan la personalización por entorno sin modificar el código base.
Módulos para Capas de Infraestructura: Separación clara entre redes, bases de datos, aplicaciones, etc., permitiendo escalar cada capa independientemente.

Esta aproximación permite gestionar infraestructura compleja de manera más ordenada, segura y mantenible a medida que crece el número de entornos y recursos


26. ¿Qué rol cumple Sentinel en el ciclo de vida de Terraform y qué tipo de políticas puede validar? 
Pregunta de integración y reflexión: 


Sentinel es un motor de políticas como código (Policy as Code) desarrollado por HashiCorp que se integra directamente con Terraform para controlar, auditar y restringir el comportamiento de la infraestructura antes de que los cambios sean aplicados.

Ventajas de Sentinel
Validación Antes de Aplicar Cambios: Permite ejecutar políticas antes de que los cambios sean aplicados, lo que ayuda a prevenir errores y problemas antes de que afecten al entorno real.
Control de Cambios: Permite restringir ciertos comportamientos o configuraciones que puedan ser perjudiciales para la infraestructura.
Integración con Terraform: Se ejecuta durante el flujo de trabajo de Terraform, lo que permite validar cambios en tiempo real.
Beneficios para la Infraestructura
Mejora la calidad de la infraestructura antes de aplicar cambios.
Ayuda a prevenir errores y problemas antes de que afecten al entorno real.
Permite mantener una infraestructura predecible y segura.
Integración con buenas prácticas DevOps
Se integra fácilmente en pipelines CI/CD junto a prácticas de GitOps y DevSecOps.
Permite mantener una infraestructura gobernada y segura.

27. ¿Cómo mejora la integración entre IaC y GitOps la trazabilidad y gobernanza de la infraestructura? 


28. ¿Qué importancia tiene el testing en infraestructura como código y qué herramientas pueden usarse para implementarlo? 

MÓDULO 8 

29. ¿Qué función cumple Backstage en una organización DevOps moderna y qué beneficios ofrece a los equipos de desarrollo? 
30. ¿Qué elementos conforman un GitOps stack típico y cómo se relacionan con Backstage? 
Pregunta de integración y reflexión: 
31. ¿Cómo mejora la trazabilidad y el control operativo al integrar CI/CD y observabilidad en Backstage? 
32. ¿Qué impacto tiene el uso de un Developer Portal como Backstage en la cultura de DevOps y la colaboración entre equipos? 

MÓDULO 9 
33. ¿Qué es FinOps y cómo se diferencia de una gestión financiera tradicional en TI? 
34. ¿Cómo ayuda AWS Cost Explorer a controlar los gastos en la nube y qué tipo de análisis permite? 
Pregunta de integración y reflexión: 
35. ¿Cómo impacta la implementación de OpenCost o Cloudability en la cultura DevOps de una organización? 
36. ¿Qué beneficios aporta aplicar principios FinOps desde etapas tempranas del desarrollo y despliegue de servicios cloud? 

MÓDULO 10 

37. ¿Cómo utiliza una plataforma AIOps la correlación de eventos para reducir el MTTR en la gestión de incidentes? 
38. Expliquen qué es la auto-remediación en el contexto de AIOps y den un ejemplo de cómo se aplicaría en un clúster de Kubernetes.
 Pregunta de integración y reflexión: 
39. ¿Por qué la Observabilidad es un pilar fundamental para que las herramientas AIOps puedan tomar decisiones de remediación efectivas?
 40. ¿De qué manera una estrategia de AIOps que reduce el MTTR puede impactar positivamente en las prácticas de FinOps y DevSecOps?

MÓDULO 11 
41. ¿Por qué es importante adaptar el lenguaje técnico al comunicarse con stakeholders no técnicos? 
42. ¿Qué elementos clave debe tener una estrategia de gestión del cambio en un proyecto tecnológico? 
Pregunta de integración y reflexión: 
43. ¿Cómo influye el liderazgo técnico en la aceptación de un cambio tecnológico dentro de un equipo o una organización? 
44. ¿Qué estrategias usarías para mantener alineados a distintos stakeholders durante un cambio que afecta la infraestructura o procesos técnicos? 

MÓDULO 12 
45. ¿Qué componentes incluiría en una arquitectura de observabilidad inteligente para identificar problemas en tiempo real con mínima intervención humana? 
46. ¿Cómo aplicaría GitOps y flujos declarativos para automatizar acciones de remediación basadas en eventos detectados por herramientas AIOps? 
47. ¿Qué criterios usaría para entrenar o configurar un sistema AIOps que priorice alertas relevantes y reduzca el ruido operacional? 
48. ¿Cómo gestionaría el cambio cultural y técnico en un equipo DevOps que nunca ha trabajado con auto-remediación o toma de decisiones asistida por IA?