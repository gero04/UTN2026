# Enunciado
**Se pide al Estudiante que analice la situación planteada y luego:**
1. Como *Product Owner* defina el Mínimo Producto Viable (MVP): **(18 puntos)**
	1. Identifique el conjunto de *User Stories* que considere deben formar parte del Mínimo Producto Viable utilizando sólo su frase verbal.
	2. Explique el alcance propuesto para el MVP y justifique la inclusión de las User Stories seleccionadas.
2. Como *Product Owner*: **(32 puntos)**
	1. Identifique **2 User Story** con su **tarjeta completa** indicando: frase verbal, descripción, criterios de aceptación y pruebas de usuario vinculadas a los requerimientos de ==*Solicitar autorización médica*== y de ==*Consultar historial médico*==. Además debe incluir la **estimación en puntos de historia** justificando los criterios utilizados para cada uno de los componentes de un punto de historia y su relación con otras *User Stories*.
	2. Indique la *User Story* que haya elegido *canónica* sólo mediante su frase verbal y justifique su elección.
Las obras sociales y centros de salud privados han experimentado un fuerte incremento en la cantidad de afiliados y en la demanda de servicios médicos digitales en los últimos años. Sin embargo, gran parte de las gestiones que realizan los socios continúan siendo por teléfonos o trámites presenciales con tiempos de respuesta prolongados. Esta situación genera dificultades tanto para los afiliados, que desean acceder rápidamente a la información clara y actualizada, como para la propia organización, que debe administrar grandes cantidades de solicitudes de manera eficiente. 
Con el objetivo de modernizar la experiencia digital y mejorar la calidad de servicio brindado, la obra social OSAC (Obra Social de Atención Cordobesa) ha decidido desarrollar una aplicación integral destinada a socios titulares y afiliados del grupo familiar. La misma estará disponible en dispositivos móviles y versión web y deberá priorizar la disponibilidad de información esencial para los afiliados durante todo momento, especialmente en situaciones relacionadas a la atención médica, autorizaciones y coberturas. 
Al iniciar sesión en la aplicación, se deberá identificar automáticamente el tipo de usuario, distinguiendo entre ==titular del grupo== familiar, ==afiliado dependiente== o ==usuario administrativo autorizado==, ya que cada perfil tendrá distintos niveles de acceso a la información y funcionalidades disponibles. Entre los datos básicos en la pantalla principal del afiliado, se incluirán su nombre completo, número de socio, plan médico activo, estado de cobertura, credencial digital para su presentación en centros médicos, próximos turnos programados y alertas relacionadas con autorizaciones o estudios pendientes. 
Una de las principales funcionalidades será asociada a la gestión digital de turnos medicos sin necesidad de intermediarios. A través de la aplicación, los usuarios podrán solicitar un turno, consultar turnos futuros, visualizar la especialidad, el profesional asignado y ubicación del centro medico, asi como cancelar o reprogramar turnos dentro de las condiciones establecidas. Determinadas prácticas podrán requerir autorizaciones previas o validaciones automáticas de cobertura antes de permitir la confirmación del turno. Cada modificación deberá impactar en tiempo real tanto en la agenda del prestador como en el historial del afiliado, generando notificaciones automáticas. Los recordatorios se enviaran con diferentes niveles de anticipación según el tipo de práctica médica. 
El sistema incorporará un modulo de gestión de autorizaciones médicas que permitirá a los afiliados solicitar, consultar y hacer seguimiento de autorizaciones para prácticas, estudios y cirugías de manera digital. Cada solicitud deberá incluir el tipo de práctica y la documentación respaldatoria en formato PDF cuando sea requerida. El sistema deberá validar automáticamente si la práctica solicitada está cubierta por el plan del afiliado, y en caso afirmativo,generar la autorización de forma inmediata. Para prácticas que requieran revisión manual por parte del área médica de OSAC, el sistema notificará al afiliado el estado de su solicitud en cada etapa del proceso, con un tiempo máximo de resolución de 48 horas hábiles. Las autorizaciones aprobadas podrán descargarse en formato PDF desde la aplicación o enviarse por correo electrónico. En caso de ser rechazadas, se especificará su motivo. 
Se prevé incorporar otro módulo clave al sistema, el cuál será de gestión del grupo familiar, disponible exclusivamente para los titulares. Desde este modulo, el titular podrá visualizar la información de cada integrante del grupo familiar, incluyendo su número de beneficiario, plan médico y estado de cobertura. Además, podrá consultar  los turnos programados  de cada afiliado dependiente y recibir alertas en su nombre. El sistema deberá distinguir con claridad qué acciones puede realizar el titular en nombre de un dependiente y cuáles requieren la acción directa del afiliado. Los afiliados dependientes tendrán acceso a su propia cuenta, pero no podrán visualizar ni modificar información de otros miembros del grupo. 
La aplicación contempla la incorporación de un módulo de farmacia a futuro que permitirá al afiliado consultar los medicamentos con cobertura incluidos en su plan, el porcentaje de descuento aplicable y las farmacias adheridas cercanas a su ubicación. Para acceder al beneficio de farmacia, el afiliado podrá presentar su credencial digital directamente desde la aplicación. El módulo de farmacia se actualizará mensualmente con el listado de medicamentos vigente, y en caso de que uno no posea cobertura o el porcentaje varíe, el sistema deberá informar al afiliado con anticipación mediante una notificación. A futuro, se prevé incorporar la recarga digital de recetas para medicaciones crónicas directamente desde la aplicación, evitando la necesidad de presentarse en la sede central de OSAC. 
Finalmente, se evalúa la incorporación del módulo de historial de atenciones y estudios, donde el afiliado podrá acceder al registro de todas las consultas médicas, internaciones y estudios realizados dentro de la red de OSAC. Cada registro deberá incluir la fecha, el prestador, la especialidad y, cuando esté disponible, los resultados de laboratorio o informes de imágenes adjuntos. Este historial será de solo lectura para el afiliado y estará ordenado cronológicamente, permitiendo filtrar por tipo de práctica o periodo de tiempo. Los informes y resultados disponibles podrán descargarse en formato PDF. Esta funcionalidad busca centralizar la información médica del afiliado en un único lugar accesible, reduciendo la necesidad de conservar documentación fisica y facilitando la consulta ante nuevos profesionales médicos. 
# Resolución propuesta (Gerónimo Vera)
## Roles
- Prestador
- Socio titular del grupo familiar
- Afiliado dependiente
- Usuario administrativo autorizado
## MVP (Minimum Viable Product)
### Descripción
Aplicación que permita la gestión digital de turnos médicos con carga de documentación respaldatoria, validación de cobertura, notificación de revisión manual por parte del área médica y notificación de rechazo de solicitudes.
No se incluye:
- Gestión del grupo familiar exclusivo para titulares
- Gestión de cobertura de farmacia
- Consulta de historial de atenciones y estudios
Plantilla:
Aplicación que permita la \[CONJUNTO DE U.S. BÁSICAS\]
No se incluye: \[CONJUNTO DE U.S. QUE SE PLANEAN PARA MAS ADELANTE\]
### Criterio
Las User Stories consideradas para el MVP permiten validar la recepción y uso de una aplicación que, a pedido de la obra social OSAC, permita a sus afiliados gestionar de manera digital la solicitud de diferentes turnos médicos. Con este fin se incluyeron funcionalidades que permiten no solo el inicio de sesión segmentado por perfiles con diferentes niveles de acceso, sino la solicitud, consulta y seguimiento de autorizaciones para prácticas, estudios y cirugías de manera digital. La posibilidad de enviar las autorizaciones aprobadas se acoto a descarga en formato PDF para validar que el usuario tenga la posibilidad de tener dicho documento. La funcionalidad relacionada con la estructura variable del registro de un usuario (sea socio titular, afiliado dependiente o usuario administrativo autorizado) no es necesaria en este momento ya que se asume que desde la obra social, en un principio, proveera los respectivos usuarios
Plantilla:
Las User Stories consideradas para el MVP permiten validar la recepción y uso de una aplicación que, a pedido de \[ORGANIZACIÓN INTERESADA\], permita a sus \[USUARIOS\] \[U.S. BÁSICA\]. Con este fin se incluyeron funcionalidades que permiten no solo \[UN POQUITO MAS DE CHAMUYO SOBRE LAS U.S.\]. La posibilidad de \[U.S. QUE TENGA UNA ESTRUCTURA O COMPORTAMIENTO VARIABLE\] se acoto a \[COMPORTAMIENTO MAS FACIL DE PROGRAMAR\] para validar que el usuario tenga la posibilidad de \[RESULTADO DE VALOR PARA EL NEGOCIO\].
## Historias de usuario incluidas en el MVP
### Socio titular del grupo familiar
#### Solicitar autorización médica
Como socio titular del grupo familiar quiero solicitar una autorización médica para programar un turno médico.
**Criterios de aceptación:**
Debe incluir el tipo de práctica
Debe incluir la documentación respaldatoria cuando sea requerida
La documentación respaldatoria debe estar en formato PDF
Si corresponde a practica que requiere revision manual notificar al afiliado en cada etapa del proceso
Tiempo maximo de resolucion de 48 horas habiles
Debe especificarse el motivo en caso de rechazar la autorizacion
**Pruebas de usuario**
Probar solicitar un turno seleccionando la especialidad (pasa)
Probar solicitar un turno sin seleccionar la especialidad (falla)
Probar solicitar un turno incluyendo la documentacion respaldatoria en formato distinto a PDF (falla)
Probar solicitar un turno sin incluir la documentacion respaldatoria (falla) 
Probar solicitar un turno para ayer (falla)
Probar solicitar un turno para una practica que no este cubierta por el plan del afiliado (falla)
**Estimación: 5**
**Justificación:**
- Complejidad: User Story compleja ya que requiere validaciones combinadas y complejas, y se trabaja con una transacción.
- Esfuerzo: Se requiere analisis, diseño e implementacion con respecto a como resolver la impresion de la autorizacion aprobada para su descarga en PDF, y tambien se requiere esfuerzo vinculado a que es un desarrollo complejo por las validaciones de si la practica esta cubierta por el plan del afiliado.
- Incertidumbre: Media. El requerimiento es claro en cuanto a proposito y no hay duda en cuanto al alcance del mismo, sin embargo no se especifican que campos debe completar el usuario a la hora de solicitar una autorizacion medica a excepcion de la practica y la documentacion respaldatoria. Con respecto a la impresion para su posterior descarga en PDF no hay duda con respecto a como generar un PDF ya que la funcionalidad puede obtenerse desde una libreria. 
#### Consultar autorización médica propia
#### Consultar autorización médica ajena
### Afiliado dependiente
#### Solicitar autorización médica
#### Consultar autorización médica propia
### Usuario administrativo autorizado
#### Solicitar autorización médica
#### Consultar autorización médica propia
## User Story Canónica
**Frase verbal**: Consultar autorización médica propia
**Justificación**: Elegí esta User Story como canónica porque en cuanto a complejidad no tiene manejo de transacciones, solamente es una consulta o lectura a una tabla donde se registran las autorizaciones médicas, en cuanto a esfuerzo es relativamente simple a la hora de programar, siendo (en el caso de la implementación Web por ejemplo) un GET a un endpoint, y por último en cuanto a la incertidumbre no tiene casi, los requerimientos lo plantean claramente.
## User Story "Consultar historial médico"
Como afiliado quiero consultar mi historial médico para acceder al registro de todas mis consultas medicas, internaciones y estudios realizados
**Criterios de aceptacion:**
El historial debe ser de solo lectura
Se debe poder filtrar por tipo de practica o periodo de tiempo
Se debe ordenar cronologicamente
Debera incluir minimamente la fecha, prestador, especialidad de la consulta medica
Debera incluir los resultados de laboratorio si estan disponibles
Debera incluir los informes de imagenes si estan disponibles
**Pruebas de aceptacion:**
Probar filtrar por un periodo de tiempo valido **PASA**
Probar filtrar por una practica existente **PASA**
Probar filtrar un periodo de tiempo invalido (fechas al revés) **FALLA**
Probar filtrar un periodo de tiempo invalido (fechas futuras) **FALLA**
Probar filtrar un periodo de tiempo invalido (fechas muy antiguas) **FALLA**
Probar filtrar una practica inexistente **FALLA**
**Estimacion:** 3
**Justificacion:**
- Complejidad: No tiene mucha complejidad, porque mas alla del apartado visual es simplemente manejar un puntero a la base de datos y ejecutar consultas
- Esfuerzo: Tiene una cantidad de esfuerzo media, debido a que hay que programar la parte de lectura de datos y diseñar la presentacion de estos, en conjunto con los filtros
- Incertidumbre: No tiene incertidumbre, los datos por los cuales se filtra estan claramente establecidos y se menciona especificamente que datos se quieren mostrar