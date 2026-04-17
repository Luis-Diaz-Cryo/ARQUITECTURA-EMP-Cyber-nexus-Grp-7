Introducción
El presente informe tiene como objetivo evaluar el nivel de cumplimiento normativo del sistema de gestión de propiedades y reservas utilizado por el cliente. Este sistema administra información relacionada con clientes, reservas, inventario y operaciones, e incluye integraciones con plataformas externas como Airbnb.
Dado que el sistema maneja datos personales, es necesario analizar su alineación con normativas nacionales e internacionales de protección de datos y seguridad de la información.
Marco Normativo Aplicable
El análisis se realizó teniendo en cuenta los siguientes marcos normativos:
•	Ley 1581 de 2012 (Colombia): regula la protección de datos personales y establece principios como legalidad, finalidad, libertad, veracidad, transparencia y seguridad. 
•	Habeas Data: garantiza el derecho de los usuarios a conocer, actualizar y rectificar su información personal. 
•	ISO/IEC 27001: estándar internacional para la gestión de la seguridad de la información, enfocado en la confidencialidad, integridad y disponibilidad. 
•	Lineamientos de buenas prácticas promovidos por entidades como el Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). 
Descripción del Sistema Evaluado
El sistema analizado corresponde a una plataforma digital que permite:
•	Gestionar propiedades en alquiler 
•	Administrar reservas y disponibilidad 
•	Manejar inventarios asociados a cada propiedad 
•	Registrar información de clientes 
•	Integrarse con plataformas externas como Airbnb para sincronización de reservas 
Actualmente, gran parte de la operación se apoya en herramientas como Excel, lo cual incrementa el riesgo de pérdida de información y falta de control.

Resultados del Análisis de Cumplimiento
A partir del checklist aplicado, se identificaron los siguientes hallazgos:
Cumplimientos Parciales
Se evidencian algunos avances iniciales en:
•	Gestión básica de información de clientes y reservas 
•	Diferenciación de tipos de usuarios (administrador, personal operativo) 
•	Intención de implementar una arquitectura tecnológica más robusta 
Sin embargo, estos aspectos no están completamente formalizados ni alineados con estándares normativos.
Brechas Identificadas
Se detectaron múltiples brechas relevantes en materia de cumplimiento:
•	Falta de consentimiento informado para el tratamiento de datos personales 
•	Ausencia de políticas de privacidad y tratamiento de datos 
•	No implementación de cifrado en almacenamiento o transmisión de información 
•	Falta de control de acceso basado en roles (RBAC) 
•	Ausencia de registros de auditoría (logs) 
•	No definición de políticas de retención de datos 
•	Limitaciones en la gestión de derechos del usuario (Habeas Data) 
Estas brechas representan riesgos significativos en términos de seguridad, cumplimiento legal y confianza del usuario.
Nivel de Madurez
El sistema presenta un nivel de madurez bajo en cumplimiento normativo, ya que la mayoría de los controles requeridos por la Ley 1581 y estándares como ISO 27001 no están implementados o se encuentran en estado inicial.
Riesgos Asociados
Las debilidades identificadas pueden generar los siguientes riesgos:
•	Exposición de datos personales de clientes 
•	Sanciones legales por incumplimiento normativo 
•	Pérdida de confianza por parte de usuarios y clientes 
•	Inconsistencias en la información de reservas 
•	Vulnerabilidad ante ataques o accesos no autorizados 
Recomendaciones
Con el fin de mejorar el cumplimiento normativo y la seguridad del sistema, se recomienda:
Protección de Datos Personales
•	Implementar mecanismos de consentimiento informado 
•	Definir y publicar una política de tratamiento de datos personales 
•	Permitir a los usuarios ejercer sus derechos de acceso, modificación y eliminación de datos 
Seguridad de la Información
•	Implementar cifrado de datos en tránsito (HTTPS) y en almacenamiento 
•	Establecer controles de acceso basados en roles (RBAC) 
•	Implementar logs y monitoreo de actividades 
Gestión Operativa
•	Definir una política de retención y eliminación de datos 
•	Implementar backups automáticos y mecanismos de recuperación 
•	Reducir la dependencia de herramientas manuales como Excel 
Integraciones Externas
•	Asegurar la integración con Airbnb mediante: 
o	validación de webhooks 
o	uso de claves API seguras 
o	control de accesos 


Resumen o conclusión llegada
El análisis realizado evidencia que el sistema actual presenta importantes oportunidades de mejora en materia de cumplimiento normativo y seguridad de la información.
Si bien la solución aún se encuentra en una etapa inicial de madurez, la adopción de una arquitectura moderna y la implementación de controles alineados con la Ley 1581 de 2012 y la norma ISO 27001 permitirán fortalecer la protección de datos, mejorar la confiabilidad del sistema y garantizar su escalabilidad futura.

