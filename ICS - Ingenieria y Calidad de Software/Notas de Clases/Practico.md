# Miercoles 26 de Agosto: SCM Y Trabajo practico 4
**Resumen en una oración:** La clase detalló los fundamentos de la Gestión de Configuración de Software para mantener la integridad del trabajo en equipo, explicó conceptos como línea base, auditorías y comités de cambios, y estableció los lineamientos para el Trabajo Práctico 4.
## Conceptos clave
- **Ítem de Configuración (IC):** Cualquier pieza o artefacto utilizado para construir un producto (código, casos de prueba, requerimientos, diagramas, base de datos, cronogramas, planes de proyecto).
- **Configuración:** Una "foto" o situación específica que se le saca al conjunto de ítems de configuración con sus versiones correspondientes en un momento dado (ej. "el 26 de agosto tenía estas cosas terminadas").
- **Versión:** Cada iteración de un mismo ítem de configuración a medida que se le van agregando cambios o mejoras (ej. Resumen ISW versión 1, versión 2).
- **Repositorio:** Lugar donde se almacenan todos los ítems de configuración con sus respectivas versiones.
- **Variante:** Ramas separadas sobre un mismo ítem de configuración para hacer pruebas y evaluar si funcionan antes de pasar a producción, con la idea de luego volver a unirlas en un solo ítem.
- **Línea Base:** Etiqueta o marca que se le pone a una configuración (conjunto de ítems) para establecer que hasta ese punto el producto es estable, fue probado, tiene calidad y cumple con lo prometido. Permite hacer un "rollback" a un punto seguro si los desarrollos futuros fallan.
- **Verificación (Física):** Evalúa si se están haciendo las cosas correctamente (ej. cumplir con la ley, nombrar el ítem como indica el plan).
- **Validación (Funcional):** Evalúa si se está haciendo la cosa correcta, es decir, si se cumple con lo que el cliente realmente pidió.
## Desarrollo de la clase
**Propósito de la Gestión de Configuración** La gestión de configuración permite trabajar en equipo garantizando que siempre se use la última versión, evitando pisar cambios, duplicarlos o generar errores al unir distintas partes del software. El objetivo fundamental de esta disciplina es cuidar la integridad del producto que se está construyendo.
**Actividades de la Gestión de Configuración** La disciplina se divide en cuatro actividades principales:
1. **Identificación** de los ítems de configuración.
2. **Control de Cambios:** Un comité evalúa si una línea base tiene defectos o requiere mejoras, analizando y aprobando modificaciones para crear una variante o una nueva línea base.
3. **Informes de Estado (Reportes):** Generación de reportes para llevar el control del proyecto.
4. **Auditorías:** Pueden ser físicas (verificación de nombres y formas documentadas) o funcionales (validación de la trazabilidad entre requerimiento, diseño, código y pruebas para asegurar que se construye lo que pidió el cliente).
**Gestión de Configuración en Procesos Definidos vs. Empíricos** Existe una diferencia clave en cómo se aplica esta disciplina según el enfoque del proyecto. En los **procesos definidos**, existe un plan documentado contra el cual auditar. Aquí cobra relevancia el **Comité de Control de Cambios**, encargado de aprobar modificaciones manuales. Nota: A diferencia de lo que apuntaste en tus notas rápidas, la profesora aclaró explícitamente que el comité de cambios es un concepto propio de procesos definidos, y generalmente no existe en procesos empíricos. En los procesos definidos, el comité se divide en:
- **Mínimo:** Para cambios menores. Conformado por roles del equipo de proyecto (líder de proyecto, arquitecto, líderes técnicos, gestor de configuración). Nunca puede ser una sola persona.
- **Ampliado:** Para cambios mayores. Es el comité mínimo más roles organizacionales (gestor de configuración de la organización, responsable de calidad, gerente de proyecto).
En los **procesos empíricos (ágiles)**, no hay una plantilla rígida contra la cual auditar de forma tradicional, ya que el proceso se define "haciendo camino al andar" mediante acuerdos del equipo, los cuales suelen ser muy estrictos. Además, se busca no gastar tiempo en actividades manuales de control que no aportan valor directo al cliente. Por ello, el control se automatiza casi por completo mediante **Prácticas Continuas (CI/CD)**. Se configuran "pipelines" (herramientas de automatización) que obligan a que el código compile y pase pruebas unitarias/integración antes de permitir un _merge_ en el repositorio común, cuidando así la integridad sin necesidad de un comité humano.
## Ejemplos y casos mencionados
- **Drive/Word:** La profesora usó el historial de versiones de Google Drive o Word como analogía de una línea base: si terminás el resumen de la Unidad 2, lo marcás; si luego la Unidad 3 sale mal, podés borrarla y volver exactamente a la configuración estable de la Unidad 2.
- **Nomenclatura de ítems:** Ejemplificó reglas de nombrado para ítems. En lugar de poner "Ejercicio práctico número 5 Charlie la fábrica de chocolate", se debe usar una lógica genérica acordada, como `ISW_Numero_TituloEjercicio` (ej. `NombreProducto_CasosDeUso_2026`).
- **Error común de repositorios:** Mencionó el caso de alumnos que subieron un repositorio de desarrollo de software (ej. un sistema de estacionamientos para la facultad) en lugar de armar un repositorio exclusivamente estructurado para gestionar los documentos de la materia.
## Puntos que el docente remarcó
- **Uso de Inteligencia Artificial:** Está permitido usar IA, pero es obligatorio revisar críticamente lo que genera. Enfatizó fuertemente que si entregan un TP con texto sin leer (ej. "reemplace el nombre de la materia aquí" o links a Wikipedia al pasar el mouse), se califica automáticamente con un 2 sin derecho a reclamo.
- **Comunicación por correo:** Se debe incluir la materia y el curso en el "Asunto" (ej. Ingeniería y Calidad de Software), usar correctamente el campo "CC" (Con Copia) y evitar los correos los viernes a la noche o con dudas que puedan resolverse en clase.
- **Diferencia entre Commit y Línea Base:** Recalcó que un _commit_ no es una línea base. El commit sube un cambio parcial de ciertos ítems, y un rollback de commit deshace todo lo modificado en él. La línea base es una "foto" integral de todos los ítems en un momento de estabilidad, y permite hacer un _tag_ (etiqueta) para volver solo a lo que se marcó como estable.
## Para el trabajo práctico / evaluación
- **Trabajo Práctico 4 (Gestión de Configuración):**
    - Se debe armar un repositorio público (o con accesos habilitados para las profesoras) en una herramienta de gestión a elección.
    - El repositorio es para gestionar los ítems de **la materia** (teórico, práctico, resoluciones), no para un proyecto de desarrollo de software.
    - Se evaluará mediante una "auditoría" donde se revisará el Plan de Gestión de Configuración de Software creado.
    - **Estructura:** Debe incluir un árbol de carpetas lógicas (ej. Teórico, Práctico).
    - **Reglas de Nombrado:** Deben definirse en una tabla que incluya: Identificación genérica del IC, Regla de nombrado (ej. `ISW_TP[N]`), Ubicación en el repositorio (directorio), y Tipo de ítem (ej. práctico, teórico). La clasificación de tipos debe ser útil (2 a 4 tipos, no 35).
    - **Líneas Base:** Se debe definir explícitamente cuándo se marcarán las líneas base, ya sea por periodicidad (ej. fines de mes) o por hitos (ej. fin de la planificación). Lo que definan, deberán cumplirlo para la entrega final del TP5.
- **Condiciones de cursada:**
    - Para regularizar: Nota 4 en los parciales y entregar todos los trabajos prácticos. Si falta entregar uno, se pierde la regularidad y no hay recuperatorio de TPs.
    - Para promocionar: 70% de los trabajos prácticos con nota 7 o superior.
    - El TP4 y TP5 se evalúan en conjunto a fin de año revisando que hayan mantenido el repositorio activo, sin subir todo a último momento ("spike").
    - **Parciales:** Son en el horario de 9 a 12 horas. No se reprograman por superposiciones, para eso está la instancia de recuperatorio.
## Dudas y cosas para revisar
- **Marcado de Línea Base en la herramienta:** Quedó de tarea para los alumnos investigar técnicamente cómo se aplica una línea base (tag) en la herramienta de repositorio que elijan (ej. Git/GitHub). La profesora aclaró que no se hace simplemente copiando carpetas ni haciendo un "commit", sino usando la funcionalidad de etiquetado/tagging de la plataforma.
Aquí tienes las notas detalladas de la clase, organizadas exactamente con la estructura solicitada y capturando toda la información técnica, ejemplos y correcciones realizadas por el docente.
---
# Miercoles 2 de Septiembre: Requerimientos Ágiles e Historias de Usuario (Caso Práctico: "Mis gastos familiares")
**Resumen en una oración:** La clase se centró en la aplicación práctica de la ingeniería de requerimientos ágiles, profundizando en la estructura, redacción y validación de Historias de Usuario (User Stories) a través del desarrollo colaborativo del caso práctico "Mis gastos familiares".
## Conceptos clave
- **Historia de Usuario (User Story)**: Descripción breve e informal de una funcionalidad, contada siempre desde la perspectiva de quien la va a usar. No reemplaza la conversación, sino que actúa como un recordatorio para detallarla.
- **Estructura estándar de la Historia de Usuario**: "Como \[rol\], quiero \[actividad/funcionalidad] de forma tal que \[valor de negocio]".
- **Las 3 C de las User Stories**:
  1. **Tarjeta (Card)**: La descripción escrita que sirve para planificar y recordar la necesidad.
  2. **Conversación**: La parte más importante. Es el diálogo entre el Product Owner (o representante del cliente) y el equipo de desarrollo para detallar la necesidad y resolver dudas.
  3. **Confirmación**: Definición de un acuerdo (Criterios de Aceptación y Pruebas) que demuestra que la característica se implementó correctamente y cumple con lo esperado.
- **Rol**: Debe ser específico del dominio o negocio (ej. "ejecutor de gasto", "responsable del gasto", "médico", "paciente"). Se debe evitar el uso genérico de "usuario del sistema" a menos que sea estrictamente necesario y no exista un rol más específico.
- **Épica**: Una historia de usuario demasiado grande que no puede ser incluida en un solo sprint. No cumple con el modelo INVEST (no es "Pequeña" ni "Estimable") y debe ser dividida en historias más pequeñas y manejables.
- **Tema (Theme)**: Conjunto de historias de usuario agrupadas conceptualmente para facilitar su estimación y planificación como una sola entidad de alto nivel.
- **Spike**: Tipo especial de historia utilizada cuando la incertidumbre (técnica o funcional) es muy alta y dificulta la estimación. Su objetivo es investigar, analizar o crear una Prueba de Concepto (POC) para reducir la incertidumbre, no entregar funcionalidad directa al usuario final. Una vez resuelta la incertidumbre, el spike se convierte en una o más user stories estimables.
- **Modelo INVEST**: Criterios de calidad para validar una buena historia de usuario:
  - **I**ndependiente (Independent): Se puede planificar e implementar en cualquier orden.
  - **N**egociable (Negotiable): No es un contrato rígido; los detalles se negocian en la conversación.
  - **V**aliosa (Valuable): Debe aportar valor de negocio al cliente o usuario final.
  - **E**stimable (Estimable): Debe tener la información suficiente para estimar su tamaño (complejidad, esfuerzo e incertidumbre).
  - **P**equeña (Small): Debe poder completarse dentro de una sola iteración (sprint).
  - **T**estable (Testable): Debe poder verificarse mediante pruebas de aceptación.
- **Criterios de Aceptación**: Reglas puntuales y objetivos que la funcionalidad debe cumplir para considerarse terminada ("Done"). Ayudan a definir los límites de la historia y a derivar las pruebas.
- **Pruebas de Aceptación**: Casos de prueba (que pueden pasar o fallar) diseñados específicamente para verificar que se cumplen los criterios de aceptación definidos.
## Desarrollo de la clase
1. **Introducción y contexto**: La clase se realizó de manera virtual debido al paro docente universitario por la falta de cumplimiento de la ley de financiamiento universitario. El docente solicitó mantener las cámaras encendidas para mejorar la interacción y la retroalimentación visual, fomentando la empatía con la situación que motiva la medida de fuerza.
2. **Repaso teórico de Requerimientos Ágiles**: Se recordó que las historias de usuario se componen de la frase verbal, los criterios de aceptación y las pruebas. Se enfatizó que la redacción debe seguir estrictamente el formato "Como \[rol], quiero \[acción] para \[valor]".
3. **Discusión sobre la especificidad de los Roles**: Ante una consulta de un alumno, el docente aclaró que el rol debe ser específico al dominio. En el caso de "Mis gastos familiares", se distinguió entre el "ejecutor de gasto" (quien registra el gasto en la app) y el "responsable del gasto" (quien realmente gastó el dinero, que puede ser otra persona, como un familiar). Usar "usuario" genérico es una mala práctica si se puede ser más específico.
4. **Diferenciación de conceptos (Épica vs. Spike)**: Se aclaró que una épica es simplemente una historia muy grande que no entra en un sprint. En cambio, un spike no tiene como resultado una funcionalidad de software, sino un documento, análisis o POC que permita estimar las historias asociadas en el futuro.
5. **Dinámica de grupos (Breakout rooms)**: Se dividió a la clase en salas para trabajar en el Trabajo Práctico N.º 1 ("Mis gastos familiares"). El objetivo era identificar y redactar las frases verbales y las historias de usuario completas para este dominio.
6. **Puesta en común y corrección en vivo**:
   - Se revisaron ejemplos de los alumnos. Un ejemplo corregido fue: *"Como gestor de gastos, quiero crear una cartera familiar para tener un lugar donde administrar y guardar los gastos familiares"*.
   - **Corrección de redacción**: El docente corrigió el uso de la frase "quiero poder". Indicó que el "poder" es redundante y debilita la redacción; debe ser directo: "quiero crear" o "quiero registrar".
   - **Atomización de historias**: Se discutió que si una historia tiene múltiples "para..." (múltiples valores de negocio) o acciones complejas, es candidata a ser dividida en dos o más historias de usuario más pequeñas.
   - **Análisis de la historia de "filtrar gastos"**: Se debatió si el valor de negocio debía ser hiperespecífico (ej. "para ver gastos de comida"). El docente guió a que el valor debe ser más general (ej. "para obtener un resumen de mis gastos bajo ciertas condiciones"), dejando los detalles específicos de los filtros (por fecha, por responsable, por monto) para los **criterios de aceptación**.
   - **Análisis de la historia de "registrar tipo de gasto"**: Se debatió si es una historia independiente o parte de "registrar un gasto". Se concluyó que tiene sentido como historia separada, ya que permite dar de alta categorías personalizadas en una iteración, para luego usarlas al registrar un gasto en una iteración posterior.
### Puesta en Común y Corrección en Vivo (El núcleo de la clase)
El docente analiza las propuestas de los grupos y realiza correcciones metodológicas en tiempo real:
- **Caso 1: Redacción redundante y doble propósito.**
    - _Propuesta del alumno:_ "Como gestor de gastos, quiero **poder** crear una cartera familiar **para** tener un lugar en donde administrar **y para** guardar los gastos familiares".
    - _Corrección 1 (Redacción):_ Eliminar la palabra "poder". Es redundante. Debe ser directo: "quiero crear".
    - _Corrección 2 (Desglose):_ La frase tiene dos "para" (dos valores de negocio distintos: "administrar" y "guardar"). **Regla del docente:** Si hay dos "para", son dos Historias de Usuario distintas. Debe dividirse.
- **Caso 2: Mezcla de funcionalidades.**
    - _Propuesta del alumno:_ "Como gestor de gastos, quiero ingresar los tipos de gastos realizados de tal forma que yo puedo asignar el gasto hacia mí o hacia otra persona".
    - _Corrección:_ El docente desarma esto en dos necesidades distintas:
        1. Registrar/Categorizar los tipos de gasto (comida, nafta, etc.).
        2. Asignar el responsable del gasto.
    - Son dos funcionalidades que deben ser dos User Stories separadas.
- **Caso 3: Dependencias y el modelo INVEST (Independiente).**
    - _Duda de un alumno:_ Si tengo una historia para "Seleccionar tipo de gasto" y otra para "Registrar tipo de gasto", ¿no violo la "I" (Independiente) de INVEST, ya que una depende de la otra?
    - _Respuesta del docente:_ No necesariamente. Para mantener la independencia, puedes desarrollar primero "Registrar un gasto" usando datos "mockeados" o pre-cargados en la base de datos (ej: "Comida", "Transporte"). No necesitas que la funcionalidad de "Crear nuevo tipo de gasto" esté terminada para poder seleccionar uno existente. Esto permite entregar valor en Sprints distintos sin bloquearse.
- **Caso 4: Criterios de Aceptación vs. Título de la Historia.**
    - _Propuesta del alumno:_ "Como ejecutor de gasto, quiero filtrar mis gastos por responsable, por rango de monto y por fecha...".
    - _Corrección:_ No pongas todos los detalles en el título. La Historia debe ser de alto nivel: _"Como \[rol], quiero consultar/visualizar mis gastos para obtener un resumen bajo ciertas condiciones"_.
    - Los detalles específicos (filtros por fecha, monto > 0, responsable) deben ir en los **Criterios de Aceptación**, no en la frase verbal.
## Ejemplos y casos mencionados
- **Caso Práctico Principal**: "Mis gastos familiares" (Trabajo Práctico N.º 1). Aplicación para registrar, categorizar y consultar gastos, permitiendo asignar el gasto a un responsable específico (que puede ser distinto de quien lo registra en el sistema).
- **Ejemplo de Historia de Usuario válida**: "Como ejecutor de gasto, quiero guardar un gasto para tener información de los gastos que realizo".
- **Ejemplo de división de historias**: Separar "Registrar tipo de gasto" de "Registrar un gasto". Primero se puede desarrollar el registro de gastos con tipos por defecto (comida, nafta, etc.), y en un sprint posterior se agrega la funcionalidad de que el usuario defina sus propios tipos de gasto personalizados.
- **Analogía del grupo de amigos (Triciclo / Splitwise)**: Se usó el ejemplo de salir con amigos y usar una app para dividir cuentas. En este escenario, una persona carga el gasto en la aplicación, pero el "responsable" del gasto puede ser otra persona del grupo (ej. "le compré una hamburguesa a Lucho"). Esto justifica la necesidad de tener dos roles distintos en el sistema.
## Puntos que el docente remarcó
- **Redacción directa**: Nunca usar "quiero poder \[hacer algo]". Debe escribirse "quiero \[hacer algo]".
- **Especificidad del Rol**: Siempre buscar el rol más específico del dominio de negocio. Evitar "usuario del sistema" como muletilla.
- **Un solo valor de negocio por historia**: Si al redactar la historia se encuentran dos "para..." distintos, es una señal de alerta de que la historia es demasiado grande y debe dividirse.
- **Objetividad en los Criterios de Aceptación**: Deben ser reglas claras y medibles (ej. "el monto debe ser un número válido mayor a cero", "la fecha no puede ser futura"), no descripciones vagas.
- **Manejo de la incertidumbre**: No forzar una estimación si hay dudas. Si hay incertidumbre técnica o de negocio, se debe proponer un *Spike* para investigar antes de estimar y desarrollar la historia real.
## Para el trabajo práctico / evaluación
- **Trabajo Práctico N.º 1**: "Mis gastos familiares".
- **Consigna**: Identificar y redactar el listado completo de Historias de Usuario para el caso. Cada historia debe incluir:
  1. Frase verbal (título resumido).
  2. Redacción completa: "Como \[rol específico], quiero \[acción] para \[valor de negocio]".
  3. Criterios de aceptación (reglas de negocio y límites).
  4. Pruebas de aceptación (escenarios de paso/fallo).
  5. Estimación en Story Points (a profundizar en la próxima clase, considerando complejidad, esfuerzo e incertidumbre).
- **Modalidad**: Se comenzó la identificación de frases verbales en grupos durante la clase. Se espera que el listado final se complete y refine aplicando las correcciones de redacción y atomización vistas en la puesta en común.
# Miercoles 9 de Septiembre: