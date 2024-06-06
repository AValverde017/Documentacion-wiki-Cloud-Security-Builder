Este proyecto será enfocado por fases. En cada fase se trabajará con unos servicios concretos de AWS principalmente para asegurarse de que quedan bien definidos los pasos a seguir según qué servicios se estén utilizando.

Enfoque de cada fase:

1. Asegurar los datos en Amazon S3: Esta fase se centra en implementar medidas de seguridad para proteger los datos almacenados en los buckets de Amazon S3. Se deben aplicar políticas de bucket, control de versiones de objeto y registros a nivel de objetos para cumplir con los requisitos de restricción de acceso (R3) y supervisión de actividad de usuario (R7).

2. Asegurar las VPC: Aquí se busca asegurar las Virtual Private Clouds (VPC) mediante la implementación de medidas de seguridad como registros de flujo de VPC, configuraciones de tabla de enrutamiento y Network Firewalls. Esto cumple con los requisitos de diseño (R1), optimización de costos (R2), restricción de acceso (R3) y resistencia a la prueba de penetración (R6).

3. Asegurar los recursos de AWS con AWS KMS: Esta fase se enfoca en implementar funciones de seguridad utilizando AWS Key Management Service (KMS) para cifrar datos almacenados en S3, EBS volumes, y datos almacenados en Secrets Manager. Esto aborda los requisitos de restricción de acceso (R3) y cifrado de datos (R5).

4. Supervisar y registrar: Finalmente, esta fase implica la implementación de funciones de supervisión y registro utilizando CloudTrail, CloudWatch y AWS Config para registrar y supervisar la actividad en la cuenta de AWS. Esto satisface los requisitos de ejecución del cumplimiento (R4), supervisión y registro de actividad del usuario (R7) y generación de alertas y notificaciones de administración (R8).
