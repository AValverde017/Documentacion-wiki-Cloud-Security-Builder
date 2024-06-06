### 5.1. Diseño general

El proyecto tiene como objetivo principal proteger los recursos de AnyCompany Financial en AWS, asegurando la confidencialidad, integridad y disponibilidad de la información sensible, particularmente la información de identificación personal (PII). Para lograr esto, se implementarán diversas soluciones de seguridad avanzadas en Amazon Web Services (AWS), que incluyen la protección de datos almacenados en Amazon S3, la seguridad de la red de la VPC, la utilización de AWS Key Management Service (KMS) para cifrado de datos y la implementación de herramientas de monitoreo y registro de actividades.

#### Componentes Clave del Proyecto

1.  **Protección de Datos en Amazon S3:**

    -   Implementación de políticas de bucket para controlar el acceso.
    -   Habilitación del control de versiones y registros de acceso a objetos.
    -   Configuración de cifrado de datos tanto en reposo como en tránsito.
    -   Utilización de Amazon S3 Inventory para la supervisión y auditoría continua de los datos almacenados.
2.  **Seguridad de la Red en la VPC:**

    -   Configuración de registros de flujo de VPC para monitorear el tráfico de red.
    -   Ajuste de tablas de enrutamiento y listas de control de acceso (ACL) para gestionar el tráfico entrante y saliente.
    -   Implementación de Network Firewalls para proteger contra accesos no autorizados y ataques.
3.  **Protección de Datos con AWS KMS:**

    -   Configuración y gestión de claves KMS administradas por el cliente para cifrar datos críticos.
    -   Aplicación de cifrado a volúmenes EBS, datos en Amazon S3 y secretos en AWS Secrets Manager.
4.  **Monitoreo y Registro de Actividades:**

    -   Implementación de AWS CloudTrail para registrar todas las actividades de API.
    -   Utilización de AWS CloudWatch para la monitorización en tiempo real y la configuración de alertas.
    -   Configuración de AWS Config para la evaluación continua de la conformidad y la supervisión de los recursos.

#### Beneficios de la Solución Propuesta

-   **Mejora en la Seguridad de los Datos:** Mediante políticas de acceso estrictas, cifrado y monitoreo continuo, se garantiza que solo las personas autorizadas tengan acceso a la información crítica.
-   **Cumplimiento Normativo:** La solución asegura que AnyCompany Financial cumpla con los estándares y regulaciones de la industria en cuanto a la protección de datos.
-   **Detección y Respuesta a Incidentes:** La configuración de alertas y registros permite la detección temprana de actividades sospechosas y la respuesta rápida a posibles incidentes de seguridad.
-   **Eficiencia Operacional:** Automatización y monitoreo continuo reducen la carga administrativa, permitiendo a los equipos de TI centrarse en otras áreas críticas.
### 5.2. Diseño detallado
#### Fase 1: Seguridad de Datos en Amazon S3

**Objetivo:** Proteger la información PII almacenada en Amazon S3 mediante políticas de acceso, cifrado y auditoría.

**Componentes y Configuraciones:**

1.  **Creación de Buckets:**

    -   **Bucket Principal:** Crear un bucket llamado `data-bucket-<unique-ID>` en la región `us-east-1` con cifrado SSE-S3 habilitado por defecto para todos los objetos.
    -   **Cargar un Objeto de Prueba:** Subir un archivo de prueba (`myfile.txt`) para verificar la configuración inicial del bucket.
2.  **Política de Bucket:**

    -   **Definición de Políticas:** Implementar una política de bucket que permita acceso solo a usuarios específicos (`voclabs`, `paulo`, `sofia`) y deniegue el acceso a cualquier otro usuario.
    -   **Pruebas de Acceso:** Verificar el acceso de los usuarios `paulo` (permitido) y `mary` (denegado) para asegurar que la política funcione correctamente.
3.  **Control de Versiones y Registro:**

    -   **Control de Versiones:** Habilitar el control de versiones en el `data-bucket` para mantener un historial de cambios de los objetos almacenados.
    -   **Registro de Acceso a Objetos:** Configurar el registro de acceso a objetos para escribir en un bucket designado (`s3-objects-access-log`), lo que permite auditar quién accede a qué objetos y cuándo.
4.  **Inventario S3:**

    -   **Configuración de Inventario:** Configurar Amazon S3 Inventory para generar informes detallados sobre los objetos almacenados, incluyendo su estado de cifrado y las configuraciones de control de versiones.

**Diagrama de Arquitectura:**

-   **Amazon S3:** Buckets con políticas de acceso, control de versiones y registro de objetos.
-   **IAM:** Usuarios y roles con permisos específicos para acceso controlado.

#### Fase 2: Seguridad de la VPC

**Objetivo:** Asegurar la red que aloja los servidores web mediante la implementación de registros de flujo y firewalls.

**Componentes y Configuraciones:**

1.  **Registros de Flujo de VPC:**

    -   **Configuración de Registros de Flujo:** Configurar registros de flujo de VPC para capturar y monitorear el tráfico de red entrante y saliente. Estos registros se almacenarán en Amazon S3 para análisis posterior.
2.  **Tablas de Enrutamiento y ACLs de Red:**

    -   **Ajuste de Configuraciones:** Revisar y ajustar las configuraciones de las tablas de enrutamiento para asegurar que solo el tráfico legítimo tenga acceso a los recursos críticos. Implementar listas de control de acceso (ACL) para definir reglas de tráfico entrante y saliente.
3.  **Network Firewalls:**

    -   **Implementación de Firewalls:** Utilizar AWS Network Firewall para proteger la VPC contra accesos no autorizados y posibles ataques. Configurar reglas de firewall para controlar el tráfico basado en políticas de seguridad de la empresa.

**Diagrama de Arquitectura:**

-   **VPC:** Redes privadas virtuales con registros de flujo y configuraciones de seguridad avanzadas.
-   **AWS Network Firewall:** Firewalls configurados para proteger contra accesos no autorizados.

#### Fase 3: Seguridad con AWS KMS

**Objetivo:** Proteger los datos almacenados y procesados utilizando claves KMS administradas por el cliente.

**Componentes y Configuraciones:**

1.  **Claves KMS:**

    -   **Creación y Gestión de Claves:** Crear claves KMS administradas por el cliente para cifrar datos sensibles. Definir políticas de uso y acceso para asegurar que solo usuarios autorizados puedan utilizar las claves.
2.  **Cifrado de Datos:**

    -   **Cifrado de Volúmenes EBS:** Aplicar cifrado a los volúmenes EBS que contienen datos críticos utilizando claves KMS.
    -   **Cifrado de Datos en Amazon S3:** Configurar el cifrado de datos en reposo en Amazon S3 utilizando claves KMS.
    -   **Cifrado en Secrets Manager:** Utilizar AWS Secrets Manager para almacenar y cifrar información sensible, como credenciales y secretos, con claves KMS.

**Diagrama de Arquitectura:**

-   **AWS KMS:** Claves gestionadas para cifrar datos críticos.
-   **EBS, S3, Secrets Manager:** Servicios cifrados utilizando claves KMS.

#### Fase 4: Supervisión y Registro

**Objetivo:** Monitorizar y registrar todas las actividades en la cuenta AWS para detectar y responder a incidentes de seguridad.

**Componentes y Configuraciones:**

1.  **AWS CloudTrail:**

    -   **Registro de Actividades de API:** Configurar AWS CloudTrail para registrar todas las actividades de API en la cuenta AWS. Estos registros se almacenarán en Amazon S3 para análisis y auditoría.
2.  **AWS CloudWatch:**

    -   **Monitorización en Tiempo Real:** Implementar AWS CloudWatch para la monitorización en tiempo real de los recursos y actividades en AWS. Configurar métricas y alarmas para detectar eventos inusuales y desencadenar acciones de respuesta.
3.  **AWS Config:**

    -   **Evaluación de Conformidad:** Utilizar AWS Config para evaluar la conformidad de los recursos con las políticas de seguridad definidas. Configurar reglas y evaluaciones continuas para asegurar que los recursos cumplan con las normativas de seguridad.

**Alertas y Notificaciones:**

-   **Configuración de Alertas:** Configurar alertas para eventos críticos utilizando Amazon SNS. Las alertas se enviarán a los administradores de seguridad para una respuesta rápida.

**Diagrama de Arquitectura:**

-   **AWS CloudTrail, CloudWatch, Config:** Servicios configurados para monitoreo y registro de actividades.
-   **SNS:** Sistema de notificaciones para alertar a los administradores de eventos críticos.